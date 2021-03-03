---
title: Trabalhar com vários contêineres usando Docker Compose
author: ghogen
description: Saiba como usar vários contêineres com Docker Compose
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 01/10/2020
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: 1dd5e237e99333e9c2fb9414b3d32ff19b70dd9b
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684274"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>Tutorial: Criar um aplicativo de vários contêineres com o Docker Compose

Neste tutorial, você aprenderá como gerenciar mais de um contêiner e se comunicar entre eles ao usar as ferramentas de contêiner no Visual Studio.  O gerenciamento de vários contêineres requer *orquestração de contêiner* e requer um orquestrador como Docker Compose, Kubernetes ou Service Fabric. Aqui, usaremos Docker Compose. Docker Compose é excelente para depuração local e testes no decorrer do ciclo de desenvolvimento.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) com o **desenvolvimento** para a Web, carga de trabalho das **Ferramentas do Azure** ou carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** instalada
::: moniker-end

::: moniker range=">= vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com **Desenvolvimento para a Web**, a carga de trabalho de **Ferramentas do Azure** e/ou **Desenvolvimento multiplataforma do .NET Core** instalados
* [Ferramentas de desenvolvimento do .NET Core 2.2](https://dotnet.microsoft.com/download/dotnet-core/2.2) para o desenvolvimento com .NET Core 2.2
* [Ferramentas de desenvolvimento do .NET Core 3](https://dotnet.microsoft.com/download/dotnet-core/3.1) para desenvolvimento com o .net Core 3,1.
::: moniker-end

## <a name="create-a-web-application-project"></a>Criar um projeto de aplicativo Web

No Visual Studio, crie um projeto de **aplicativo web ASP.NET Core** , chamado `WebFrontEnd` , para criar um aplicativo Web com páginas Razor.
  
::: moniker range="vs-2017"

Não selecione **Habilitar Suporte ao Docker**. Você adicionará suporte do Docker mais tarde.

![Captura de tela da criação do projeto Web](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range="vs-2019"

![Criar ASP.NET Core projeto de aplicativo Web](./media/tutorial-multicontainer/vs-2019/create-web-project1.png)

Não selecione **Habilitar Suporte ao Docker**. Você adicionará suporte do Docker mais tarde.

![Captura de tela de informações adicionais durante a criação de um projeto Web. A opção para habilitar o suporte ao Docker não está selecionada.](./media/tutorial-multicontainer/vs-2019/create-web-project-additional-information.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>Criar um projeto de API Web

Adicione um projeto à mesma solução e chame-o de *MyWebAPI*. Selecione **API** como o tipo de projeto e desmarque a caixa de seleção **Configurar para https**. Nesse design, estamos usando SSL apenas para comunicação com o cliente, não para comunicação entre contêineres no mesmo aplicativo Web. O só `WebFrontEnd` precisa de HTTPS e o código nos exemplos pressupõe que você tenha desmarcado essa caixa de seleção. Em geral, os certificados de desenvolvedor .NET usados pelo Visual Studio só têm suporte para solicitações externas para contêiner, não para solicitações de contêiner para contêiner.

::: moniker range="vs-2017"
   ![Captura de tela da criação do projeto de API Web](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range="vs-2019"
   ![Captura de tela da criação do projeto de API Web](./media/tutorial-multicontainer/vs-2019/create-web-api-project.png)
::: moniker-end

## <a name="add-code-to-call-the-web-api"></a>Adicionar código para chamar a API da Web

1. No `WebFrontEnd` projeto, abra o arquivo *index.cshtml.cs* e substitua o `OnGet` método pelo código a seguir.

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

    Com o .NET Core 3,1, você não precisa disso, pois você pode usar a API WeatherForecast que já está lá. No entanto, você precisa comentar a chamada para <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*>  no `Configure` método em *Startup.cs*, pois esse código usa http, não HTTPS, para chamar a API da Web.

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

   O arquivo *. dockerignore* contém tipos de arquivo e extensões que você não deseja que o Docker inclua no contêiner. Esses arquivos são geralmente associados ao ambiente de desenvolvimento e ao controle do código-fonte, e não a parte do aplicativo ou serviço que você está desenvolvendo.

   Examine a seção **ferramentas de contêiner** do painel de saída para obter detalhes dos comandos que estão sendo executados.  Você pode ver a ferramenta de linha de comando Docker-Compose é usada para configurar e criar os contêineres de tempo de execução.

1. No projeto de API Web, clique com o botão direito do mouse no nó do projeto e escolha **Adicionar**  >  **suporte ao orquestrador de contêiner**. Escolha **Docker Compose** e, em seguida, selecione o mesmo so de destino.  

    > [!NOTE]
    > Nesta etapa, o Visual Studio oferecerá a criação de um Dockerfile. Se você fizer isso em um projeto que já tem o suporte do Docker, será perguntado se deseja substituir o Dockerfile existente. Se você tiver feito alterações em seu Dockerfile que deseja manter, escolha não.

    O Visual Studio faz algumas alterações no arquivo YML do Docker Compose. Agora, ambos os serviços estão incluídos.

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

1. Execute o site localmente agora (F5 ou CTRL + F5) para verificar se ele funciona conforme o esperado. Se tudo estiver configurado corretamente com a versão do .NET Core 2. x, você verá a mensagem "Olá de WebFrontEnd e webAPI (com valor 1)".  Com o .NET Core 3, você vê dados de previsão do tempo.

   O primeiro projeto que você usa ao adicionar orquestração de contêiner é configurado para ser iniciado quando você executa ou depura. Você pode configurar a ação de inicialização nas **Propriedades do projeto** para o projeto Docker-Compose.  No nó do projeto Docker-Compose, clique com o botão direito do mouse para abrir o menu de contexto e escolha **Propriedades** ou use Alt + Enter.  A captura de tela a seguir mostra as propriedades que você deseja para a solução usada aqui.  Por exemplo, você pode alterar a página que é carregada Personalizando a propriedade de **URL de serviço** .

   ![Captura de tela das propriedades do projeto Docker-Compose](media/tutorial-multicontainer/launch-action.png)

   Veja o que você vê quando o é iniciado (a versão do .NET Core 2. x):

   ![Captura de tela da execução do aplicativo Web](media/tutorial-multicontainer/webfrontend.png)

   O aplicativo Web para .NET 3,1 mostra os dados meteorológicos no formato JSON.

## <a name="next-steps"></a>Próximas etapas

Examine as opções para implantar seus [contêineres no Azure](/azure/containers).

## <a name="see-also"></a>Confira também
  
[Docker Compose](https://docs.docker.com/compose/)  
[Ferramentas de contêiner](./index.yml)