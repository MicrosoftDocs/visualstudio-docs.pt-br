---
title: Tutorial – Criar um aplicativo de vários contêineres com o Docker Compose
description: Saiba como gerenciar mais de um contêiner e se comunicar entre eles no Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 06/17/2019
ms.topic: tutorial
ms.openlocfilehash: 03adc2385c202710425fbc8e6b12c832526b5f90
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938943"
---
# <a name="create-a-multi-container-app-with-docker-compose"></a>Criar um aplicativo de vários contêineres com o Docker Compose

Neste tutorial, você aprenderá a gerenciar mais de um contêiner e a se comunicar entre eles ao usar o Docker Compose no Visual Studio para Mac.

## <a name="prerequisites"></a>Pré-requisitos

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio para Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="create-an-aspnet-core-web-application-and-add-docker-support"></a>Criar um Aplicativo Web ASP.NET Core e adicionar suporte ao Docker

1. Crie uma nova solução acessando **Arquivo > Nova Solução**.
1. Em **.NET Core > aplicativo** , escolha o modelo de **aplicativo Web** : ![ criar um novo aplicativo ASP.net](media/docker-quickstart-1.png)
1. Selecione a estrutura de destino. Neste exemplo, usaremos o .NET Core 2,2: ![ definir estrutura de destino](media/docker-quickstart-2.png)
1. Insira os detalhes do projeto, como o Nome do Projeto (_DockerDemoFrontEnd_ neste exemplo) e o Nome da Solução (_DockerDemo_). O projeto criado contém todos os princípios necessários para compilar e executar um site do ASP.NET Core.
1. Na Painel de Soluções, clique com o botão direito do mouse no projeto DockerDemoFrontEnd e selecione **adicionar > adicionar suporte ao Docker**: ![ Adicionar suporte ao Docker](media/docker-quickstart-3.png)

O Visual Studio para Mac vai adicionar automaticamente um novo projeto à sua solução denominado **docker-compose** e um **Dockerfile** ao seu projeto existente.

## <a name="create-an-aspnet-core-web-api-and-add-docker-support"></a>Criar uma API Web ASP.NET Core e adicionar suporte ao Docker

Em seguida, criaremos um segundo projeto que atuará como nossa API de back-end. O modelo **API do .NET Core** inclui um controlador que nos permite lidar com solicitações RESTful.

1. Adicione um novo projeto à solução existente clicando com botão direito na solução e escolhendo **Adicionar > Adicionar Novo Projeto**.
1. Em **.NET Core > Aplicativo**, escolha o modelo **API**.
1. Selecione a estrutura de destino. Neste exemplo, usaremos o .NET Core 2.2
1. Insira os detalhes do projeto, como o Nome do Projeto (_DockerDemoAPI_ neste exemplo).
1. Uma vez criado, vá para o Painel de Soluções, clique com o botão direito do mouse no projeto DockerDemoAPI e selecione **Adicionar > Adicionar Suporte ao Docker**.

O arquivo **docker-compose.yml** no projeto **docker-compose** será automaticamente atualizado para incluir o projeto de API com o projeto de aplicativo Web existente. Quando compilamos e executamos o projeto **docker-compose**, cada um desses projetos é implantado em um contêiner do Docker separado.

```
version: '3.4'

services:
  dockerdemofrontend:
    image: ${DOCKER_REGISTRY-}dockerdemofrontend
    build:
      context: .
      dockerfile: DockerDemoFrontEnd/Dockerfile

  dockerdemoapi:
    image: ${DOCKER_REGISTRY-}dockerdemoapi
    build:
      context: .
      dockerfile: DockerDemoAPI/Dockerfile
```

## <a name="integrate-the-two-containers"></a>Integrar os dois contêineres

Agora temos dois projetos ASP.NET em nossa solução e ambos estão configurados com suporte ao Docker. Em seguida, precisamos adicionar algum código!

1. No projeto `DockerDemoFrontEnd`, abra o arquivo *Index.cshtml.cs* e substitua o método `OnGet` pelo seguinte código:

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://dockerdemoapi/api/values/1");
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```

1. No arquivo *Index.cshtml*, adicione uma linha para exibir `ViewData["Message"]` de modo que o arquivo se pareça com o seguinte código:

      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }

      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="https://docs.microsoft.com/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. Agora, no projeto de API Web, adicione código ao controlador Valores para personalizar a mensagem retornada pela API para a chamada que você adicionou de *webfrontend*:

      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

1. Defina o projeto `docker-compose` como o projeto de inicialização e vá para **Executar > Iniciar Depuração**. Se tudo estiver configurado corretamente, você verá a mensagem "Olá do webfrontend e webapi (com o valor 1).":

![Execução da solução de vários contêineres do Docker](media/docker-multicontainer-debug.png)
