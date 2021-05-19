---
title: Trabalhar com vários contêineres usando Docker Compose
author: ghogen
description: Saiba como usar vários contêineres com Docker Compose
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 03/15/2021
ms.technology: vs-azure
ms.topic: tutorial
ms.openlocfilehash: 43684288eea2e1864bf31a8bb68bbac1b217a976
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973272"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>Tutorial: Criar um aplicativo de vários contêineres com o Docker Compose

Neste tutorial, você aprenderá a gerenciar mais de um contêiner e a se comunicar entre eles ao usar as Ferramentas de Contêiner Visual Studio.  O gerenciamento de vários contêineres requer *orquestração* de contêineres e requer um orquestrador como Docker Compose, Kubernetes ou Service Fabric. Aqui, vamos usar Docker Compose. Docker Compose é ótimo para depuração local e teste no decorrer do ciclo de desenvolvimento.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) com a carga de trabalho Desenvolvimento **para Web,** Ferramentas do **Azure** ou desenvolvimento de plataforma cruzada **do .NET Core** instalada
::: moniker-end

::: moniker range=">= vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com **Desenvolvimento para a Web**, a carga de trabalho de **Ferramentas do Azure** e/ou **Desenvolvimento multiplataforma do .NET Core** instalados
* [Ferramentas de desenvolvimento do .NET Core 2.2](https://dotnet.microsoft.com/download/dotnet-core/2.2) para o desenvolvimento com .NET Core 2.2
* [Ferramentas de desenvolvimento do .NET Core 3](https://dotnet.microsoft.com/download/dotnet-core/3.1) para desenvolvimento com o .NET Core 3.1.
::: moniker-end

## <a name="create-a-web-application-project"></a>Criar um projeto de aplicativo Web

No Visual Studio, crie um **projeto ASP.NET Core Web App,** chamado , para criar um aplicativo Web com páginas `WebFrontEnd` razor.
  
::: moniker range="vs-2017"

Não selecione **Habilitar Suporte ao Docker**. Você adicionará o suporte ao Docker mais tarde.

![Captura de tela da criação do projeto Web](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range="vs-2019"

![Criar ASP.NET Projeto de Aplicativo Web Core](./media/tutorial-multicontainer/vs-2019/create-web-project1.png)

Não selecione **Habilitar Suporte ao Docker**. Você adicionará o suporte ao Docker mais tarde.

![Captura de tela da tela Informações adicionais ao criar um projeto Web. A opção Habilitar Suporte ao Docker não está selecionada.](./media/tutorial-multicontainer/vs-2019/create-web-project-additional-information.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>Criar um projeto de API Web

Adicione um projeto à mesma solução e chame-o *de MyWebAPI*. Selecione **API** como o tipo de projeto e des marque a caixa de seleção **Configurar para HTTPS.** Nesse design, estamos usando apenas sSL para comunicação com o cliente, não para comunicação entre contêineres no mesmo aplicativo Web. O só `WebFrontEnd` precisa de HTTPS e o código nos exemplos pressupõe que você tenha desmarcado essa caixa de seleção. Em geral, os certificados de desenvolvedor .NET usados pelo Visual Studio só têm suporte para solicitações externas para contêiner, não para solicitações de contêiner para contêiner.

::: moniker range="vs-2017"
   ![Captura de tela da criação do projeto de API Web](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range="vs-2019"
   ![Captura de tela da criação do projeto de API Web](./media/tutorial-multicontainer/vs-2019/create-webapi-project.png)
::: moniker-end

## <a name="add-code-to-call-the-web-api"></a>Adicionar código para chamar a API da Web

1. No `WebFrontEnd` projeto, abra o arquivo *index. cshtml. cs* e substitua o `OnGet` método pelo código a seguir.

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          // request.RequestUri = new Uri("http://mywebapi/WeatherForecast"); // ASP.NET 3 (VS 2019 only)
          request.RequestUri = new Uri("http://mywebapi/api/values/1"); // ASP.NET 2.x
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > No código do mundo real, você não deve descartar `HttpClient` após cada solicitação. Para obter as práticas recomendadas, consulte [usar HttpClientFactory para implementar solicitações HTTP resilientes](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests).

   Para o .NET Core 3,1 no Visual Studio 2019 ou posterior, o modelo de API da Web usa uma API WeatherForecast, portanto, remova a marca de comentário dessa linha e comente a linha para ASP.NET 2. x.

1. No arquivo *Index.cshtml*, adicione uma linha para exibir `ViewData["Message"]` de modo que o arquivo se pareça com o seguinte código:
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. (Somente ASP.NET 2. x) Agora, no projeto de API Web, adicione o código ao controlador de valores para personalizar a mensagem retornada pela API para a chamada que você adicionou do *WebFrontEnd*.
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

    Com o .NET Core 3,1, você não precisa disso, pois você pode usar a API WeatherForecast que já está lá. No entanto, você precisa comentar a chamada para <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*>  no `Configure` método em *Startup. cs*, pois esse código usa http, não HTTPS, para chamar a API da Web.

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. No `WebFrontEnd` projeto, escolha **Adicionar > contêiner de suporte do orquestrador**. A caixa de diálogo **Opções de suporte do Docker** é exibida.

1. Escolha **Docker Compose**.

1. Escolha o so de destino, por exemplo, Linux.

   ![Captura de tela da escolha do sistema operacional de destino](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   O Visual Studio cria um arquivo *Docker-Compose. yml* e um arquivo *. dockerignore* no nó **Docker-Compose** na solução, e esse projeto é mostrado na fonte negrito, que mostra que é o projeto de inicialização.

   ![Captura de tela de Gerenciador de Soluções com o projeto Docker-Compose adicionado](media/tutorial-multicontainer/multicontainer-solution-explorer.png)

   O *Docker-Compose. yml* aparece da seguinte maneira:

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   O *arquivo .dockerignore* contém tipos de arquivo e extensões que você não deseja que o Docker inclua no contêiner. Esses arquivos geralmente são associados ao ambiente de desenvolvimento e ao controle do código-fonte, não fazem parte do aplicativo ou serviço que você está desenvolvendo.

   Veja a seção **Ferramentas de** Contêiner do painel de saída para obter detalhes dos comandos que estão sendo executados.  Você pode ver que a ferramenta de linha de comando docker-compose é usada para configurar e criar os contêineres de runtime.

1. No projeto de API Web, clique novamente com o botão direito do mouse no nó do projeto e escolha **Adicionar Suporte**  >  **ao Orquestrador de Contêineres.** Escolha **Docker Compose** e selecione o mesmo sistema operacional de destino.  

    > [!NOTE]
    > Nesta etapa, o Visual Studio oferecerá para criar um Dockerfile. Se você fizer isso em um projeto que já tem suporte do Docker, será solicitado se deseja substituir o Dockerfile existente. Se você tiver feito alterações no Dockerfile que deseja manter, escolha não.

    Visual Studio faz algumas alterações no arquivo YML do Docker Compose. Agora, ambos os serviços estão incluídos.

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. Execute o site localmente agora (F5 ou Ctrl+F5) para verificar se ele funciona conforme o esperado. Se tudo estiver configurado corretamente com a versão do .NET Core 2.x, você verá a mensagem "Olá de webfrontend e webapi (com o valor 1)."  Com o .NET Core 3, você vê dados de previsão do tempo.

   O primeiro projeto que você usa ao adicionar a orquestração de contêiner é definido para ser lançado quando você executar ou depurar. Você pode configurar a ação de lançamento nas **Propriedades do Projeto** para o projeto docker-compose.  No nó do projeto docker-compose, clique com o botão direito do mouse para abrir o menu de contexto e, em seguida, escolha **Propriedades** ou use Alt+Enter.  A captura de tela a seguir mostra as propriedades que você deseja para a solução usada aqui.  Por exemplo, você pode alterar a página carregada personalização da **propriedade URL do** Serviço.

   ![Captura de tela das propriedades do projeto docker-compose](media/tutorial-multicontainer/launch-action.png)

   Veja o que você vê quando o é iniciado (a versão do .NET Core 2. x):

   ![Captura de tela da execução do aplicativo Web](media/tutorial-multicontainer/webfrontend.png)

   O aplicativo Web para .NET 3,1 mostra os dados meteorológicos no formato JSON.

## <a name="next-steps"></a>Próximas etapas

Examine as opções para implantar seus [contêineres no Azure](/azure/containers).

Para obter mais controle sobre quais serviços são iniciados durante uma sessão de depuração, saiba como usar Docker Compose perfis de inicialização para configurar quais serviços são executados durante a depuração. Consulte [gerenciar perfis de inicialização para Docker Compose](launch-profiles.md)

## <a name="see-also"></a>Confira também
  
[Docker Compose](https://docs.docker.com/compose/)  
[Ferramentas de contêiner](./index.yml)