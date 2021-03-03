---
title: Ferramentas de contêiner do Visual Studio com ASP.NET Core e React.js
titleSuffix: ''
ms.custom: SEO-VS-2020
author: ghogen
description: Saiba como criar um aplicativo de SPA em contêineres com ferramentas de contêiner do Visual Studio e Docker
ms.author: ghogen
ms.date: 02/21/2021
ms.technology: vs-azure
ms.topic: quickstart
ms.openlocfilehash: 7a2a9e7c8b2c53dcee7f11d4b0b795b66ab80a80
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684337"
---
# <a name="quickstart-use-docker-with-a-react-single-page-app-in-visual-studio"></a>Início rápido: usar o Docker com um aplicativo de página única reagir no Visual Studio

Com o Visual Studio, você pode criar, depurar e executar aplicativos do ASP.NET Core facilmente em contêineres, incluindo aqueles com aplicativo de página única do React.js, e publicá-los no ACR (Registro de Contêiner do Azure), no Docker Hub, no Serviço de Aplicativo do Azure ou no seu próprio registro de contêiner. Neste artigo, publicaremos no ACR.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) com as workloads **Desenvolvimento para a Web**, **Ferramentas do Azure** e/ou **Desenvolvimento multiplataforma do .NET Core** instaladas
* Para publicar no Registro de Contêiner do Azure, uma assinatura do Azure. [Inscreva-se em uma avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p/).
* [Node.js](https://nodejs.org/en/download/)
* Para contêineres do Windows, Windows 10 versão 1903 ou posterior, para usar as imagens do Docker referenciadas neste artigo.
::: moniker-end
::: moniker range=">=vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com **Desenvolvimento para a Web**, a carga de trabalho de **Ferramentas do Azure** e/ou **Desenvolvimento multiplataforma do .NET Core** instalados
* [Ferramentas de desenvolvimento do .net core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1) para desenvolvimento com o .net Core 3,1.
* Para publicar no Registro de Contêiner do Azure, uma assinatura do Azure. [Inscreva-se em uma avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p/).
* [Node.js](https://nodejs.org/en/download/)
* Para contêineres do Windows, Windows 10 versão 1903 ou posterior, para usar as imagens do Docker referenciadas neste artigo.
::: moniker-end

## <a name="installation-and-setup"></a>Instalação e configuração

Para a instalação do Docker, primeiro examine as informações no [Docker desktop para Windows: o que saber antes de instalar](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)o. Em seguida, instale o [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

## <a name="create-a-project-and-add-docker-support"></a>Criar um projeto e adicionar suporte ao Docker

::: moniker range="vs-2017"
1. Clique em um novo projeto, usando o modelo do **Aplicativo Web ASP.NET Core**.
1. Selecione **React.js**. Não é possível selecionar **Habilitar suporte ao Docker**, mas não se preocupe, você pode adicionar esse suporte depois de criar o projeto.

   ![Captura de tela do novo projeto React.js](media/container-tools-react/vs-2017/new-react-project.png)

1. Clique com botão direito do mouse no nó do projeto e escolha **Adicionar** > **Suporte ao Docker** para adicionar um Dockerfile ao seu projeto.

   ![Adicionar suporte ao Docker](media/container-tools-react/vs-2017/add-docker-support.png)

1. Selecione o tipo de contêiner e clique em **OK**.
::: moniker-end

::: moniker range=">=vs-2019"

1. Crie um novo projeto usando o **ASP.NET Core com React.js** modelo.

   ![Captura de tela da criação de um novo projeto de React.js](media/container-tools-react/vs-2019/create-reactjs-project.png)

1. Na tela **informações adicionais** , não é possível selecionar **habilitar suporte do Docker**, mas não se preocupe, você pode adicionar esse suporte mais tarde.

   ![Captura de tela da criação de um novo projeto de React.js-telas de informações adicionais](media/container-tools-react/vs-2019/new-react-project-additional-information.png)

1. Clique com botão direito do mouse no nó do projeto e escolha **Adicionar** > **Suporte ao Docker** para adicionar um Dockerfile ao seu projeto.

   ![Adicionar suporte ao Docker](media/container-tools-react/vs-2017/add-docker-support.png)

1. Selecione o tipo de contêiner.
::: moniker-end

A próxima etapa é diferente, dependendo se você estiver usando contêineres do Linux ou contêineres do Windows.

## <a name="modify-the-dockerfile-linux-containers"></a>Modificar o Dockerfile (contêineres do Linux)

Um *Dockerfile*, ou seja, a receita para criar uma imagem final do Docker, é criado no projeto. Consulte a [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para obter uma compreensão dos comandos dentro dele.

Abra o *Dockerfile* no projeto e adicione as linhas a seguir para instalar o Node.js 10.x no contêiner. Certifique-se de adicionar essas linhas na primeira seção, para adicionar a instalação do Gerenciador de pacotes do nó *npm.exe* à imagem base, bem como na `build` seção.

```Dockerfile
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
```

O *Dockerfile* deve se parecer com o seguinte:

```Dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
WORKDIR /src
COPY ["WebApplication-ReactSPA/WebApplication-ReactSPA.csproj", "WebApplication-ReactSPA/"]
RUN dotnet restore "WebApplication-ReactSPA/WebApplication-ReactSPA.csproj"
COPY . .
WORKDIR "/src/WebApplication-ReactSPA"
RUN dotnet build "WebApplication-ReactSPA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication-ReactSPA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication-ReactSPA.dll"]
```

O *Dockerfile* anterior é baseado na imagem [MCR.Microsoft.com/dotnet/Core/ASPNET](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) e inclui instruções para modificar a imagem base criando seu projeto e adicionando-o ao contêiner.

Quando a caixa de seleção **Configurar para HTTPS** do novo projeto estiver marcada, o *Dockerfile* exibirá duas portas. Uma porta é usada para o tráfego HTTP; a outra porta é usada para o HTTPS. Se a caixa de seleção não estiver marcada, uma única porta (80) será exposta para o tráfego HTTP.

## <a name="modify-the-dockerfile-windows-containers"></a>Modificar o Dockerfile (contêineres do Windows)

Abra o arquivo de projeto clicando duas vezes no nó do projeto e atualize o arquivo de projeto (*. csproj) adicionando a seguinte propriedade como um filho do `<PropertyGroup>` elemento:

   ```xml
    <DockerfileFastModeStage>base</DockerfileFastModeStage>
   ```

Atualize o Dockerfile adicionando as linhas a seguir. Isso copiará o nó e o NPM para o contêiner.

   1. Adicionar ``# escape=` `` à primeira linha do Dockerfile
   1. Adicione as seguintes linhas antes de `FROM … base`

      ```Dockerfile
      FROM mcr.microsoft.com/powershell:nanoserver-1903 AS downloadnodejs
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      Expand-Archive nodejs.zip -DestinationPath C:\; `
      Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs
      ```

   1. Adicione a seguinte linha antes e depois de `FROM … build`

      ```Dockerfile
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      ```

   1. O Dockerfile completo agora deve ser semelhante a este:

      ```Dockerfile
      # escape=`
      #Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
      #For more information, please see https://aka.ms/containercompat
      FROM mcr.microsoft.com/powershell:nanoserver-1903 AS downloadnodejs
      RUN mkdir -p C:\nodejsfolder
      WORKDIR C:\nodejsfolder
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      Expand-Archive nodejs.zip -DestinationPath C:\; `
      Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs

      FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1903 AS base
      WORKDIR /app
      EXPOSE 80
      EXPOSE 443
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\

      FROM mcr.microsoft.com/dotnet/core/sdk:3.1-nanoserver-1903 AS build
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      WORKDIR /src
      COPY ["WebApplicationReact1/WebApplicationReact1.csproj", "WebApplicationReact1/"]
      RUN dotnet restore "WebApplicationReact1/WebApplicationReact1.csproj"
      COPY . .
      WORKDIR "/src/WebApplicationReact1"
      RUN dotnet build "WebApplicationReact1.csproj" -c Release -o /app/build

      FROM build AS publish
      RUN dotnet publish "WebApplicationReact1.csproj" -c Release -o /app/publish

      FROM base AS final
      WORKDIR /app
      COPY --from=publish /app/publish .
      ENTRYPOINT ["dotnet", "WebApplicationReact1.dll"]
      ```

   1. Atualize o arquivo. dockerignore removendo o `**/bin` .

## <a name="debug"></a>Depurar

Selecione **Docker** no menu suspenso de depuração na barra de ferramentas e inicie a depuração do aplicativo. Poderá aparecer uma mensagem com um aviso sobre a confiança em um certificado, escolha confiar no certificado para continuar.  Na primeira vez que você cria, o Docker baixa as imagens base, portanto, pode demorar um pouco mais.

A opção **Ferramentas de Contêiner** na janela **Saída** mostra quais ações estão ocorrendo. Você deve ver as etapas de instalação associadas a *npm.exe*.

O navegador mostra a página inicial do aplicativo.

::: moniker range="vs-2017"
   ![Captura de tela do aplicativo em execução](media/container-tools-react/vs-2017/running-app.png)
::: moniker-end
::: moniker range=">=vs-2019"
   ![Captura de tela do aplicativo em execução](media/container-tools-react/vs-2019/running-app.png)
::: moniker-end

Tente navegar até a página *Contador* e teste o código do contador no lado do cliente clicando no botão **Incremento**.

Abra o **PMC** (console do gerenciador de pacotes) no menu **Ferramentas**> Gerenciador de Pacotes NuGet, **Console do Gerenciador de Pacotes**.

A imagem resultante do Docker do aplicativo é marcada como *dev*. A imagem é baseada na marca *3,1-los-1903* da imagem base *dotnet/principal/ASPNET* . Execute o comando `docker images` na janela do PMC **(Console do Gerenciador de Pacotes)**. As imagens no computador são exibidas:

```console
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
webapplicationreact1                   dev                 09be6ec2405d        2 hours ago         352MB
mcr.microsoft.com/dotnet/core/aspnet   3.1-buster-slim     e3559b2d50bb        10 days ago         207MB
```

> [!NOTE]
> A imagem **dev** não contém os binários do aplicativo e outros tipos de conteúdo, pois as configurações de **depuração** usam montagem de volume para fornecer a experiência iterativa de edição e depuração. Para criar uma imagem de produção que contém todo o conteúdo, use a configuração de **Versão**.

Execute o comando `docker ps` no PMC. Observe que o aplicativo está em execução usando o contêiner:

```console
CONTAINER ID        IMAGE                      COMMAND               CREATED             STATUS              PORTS                                           NAMES
56d1b1008c89        webapplicationreact1:dev   "tail -f /dev/null"   2 hours ago         Up 2 hours          0.0.0.0:32771->80/tcp, 0.0.0.0:32770->443/tcp   WebApplication-React1
```

## <a name="publish-docker-images"></a>Publicar imagens do Docker

Depois que o ciclo de desenvolvimento e de depuração do aplicativo forem concluídos, você poderá criar uma imagem de produção do aplicativo.

:::moniker range="vs-2017"

1. Altere a lista suspensa de configuração para **Versão** e compile o aplicativo.
1. Clique com o botão direito no projeto em **Gerenciador de Soluções** e escolha **Publicar**.
1. Na caixa de diálogo destino de publicação, selecione **registro de contêiner**.
1. Escolha **Criar Registro de Contêiner do Azure** e clique em **Publicar**.
1. Preencha os valores desejados em **Criar um novo Registro de Contêiner do Azure**.

    | Configuração      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Prefixo DNS** | Nome globalmente exclusivo | Nome que identifica exclusivamente o registro de contêiner. |
    | **Assinatura** | Escolha sua assinatura | A assinatura do Azure a utilizar. |
    | **[Grupo de Recursos](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  Nome do grupo de recursos no qual criar o registro de contêiner. Escolha **Novo** para criar um novo grupo de recursos.|
    | **[SKU](/azure/container-registry/container-registry-skus)** | Standard | Camada de serviço do registro de contêiner  |
    | **Local do Registro** | Um local próximo | Escolha um Local em uma [região](https://azure.microsoft.com/regions/) próxima a você ou perto de outros serviços que usarão o registro de contêiner. |

    ![Caixa de diálogo Criar um Registro de Contêiner do Azure do Visual Studio](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png)

1. Selecione **Criar**.

   ![Captura de tela mostrando a publicação bem-sucedida](media/container-tools/publish-succeeded.png)
:::moniker-end

:::moniker range=">=vs-2019"

1. Altere a lista suspensa de configuração para **Versão** e compile o aplicativo.
1. Clique com o botão direito no projeto em **Gerenciador de Soluções** e escolha **Publicar**.
1. Na caixa de diálogo Publicar destino, selecione **registro de contêiner do Docker**.

   ![Escolher registro de contêiner do Docker](media/container-tools-react/vs-2019/publish-dialog1.png)

1. Em seguida, escolha **registro de contêiner do Azure**.

   ![Escolher registro de contêiner do Azure](media/container-tools-react/vs-2019/publish-dialog-acr.png)

1. Escolha **criar um novo registro de contêiner do Azure**.
1. Preencha os valores desejados na tela **criar novo registro de contêiner do Azure** .

    | Configuração      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Prefixo DNS** | Nome globalmente exclusivo | Nome que identifica exclusivamente o registro de contêiner. |
    | **Assinatura** | Escolha sua assinatura | A assinatura do Azure a utilizar. |
    | **[Grupo de Recursos](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  Nome do grupo de recursos no qual criar o registro de contêiner. Escolha **Novo** para criar um novo grupo de recursos.|
    | **[SKU](/azure/container-registry/container-registry-skus)** | Standard | Camada de serviço do registro de contêiner  |
    | **Local do Registro** | Um local próximo | Escolha um Local em uma [região](https://azure.microsoft.com/regions/) próxima a você ou perto de outros serviços que usarão o registro de contêiner. |

    ![Caixa de diálogo Criar um Registro de Contêiner do Azure do Visual Studio](media/container-tools-react/vs-2019/azure-container-registry-details.png)

1. Selecione **criar** e, em seguida, selecione **concluir**.

   ![Selecionar ou criar um novo ACR](media/container-tools-react/vs-2019/publish-dialog2.png)

   Quando o processo de publicação termina, você pode revisar as configurações de publicação e editá-las, quando necessário, ou publicar a imagem novamente usando o botão **publicar** .

   ![Captura de tela mostrando a publicação bem-sucedida](media/container-tools-react/vs-2019/publish-finished.png)

   Para iniciar novamente usando a caixa de diálogo **publicar** , exclua o perfil de publicação usando o link **excluir** nesta página e escolha **publicar** novamente.
:::moniker-end

## <a name="next-steps"></a>Próximas etapas

Agora, é possível extrair o contêiner do registro para qualquer host capaz de executar imagens do Docker, por exemplo [Instâncias de Contêiner do Azure](/azure/container-instances/container-instances-tutorial-deploy-app).

## <a name="additional-resources"></a>Recursos adicionais

* [Desenvolvimento de contêiner com o Visual Studio](./index.yml)
* [Solucionar problemas de desenvolvimento do Visual Studio com o Docker](troubleshooting-docker-errors.md)
* [Repositório do GitHub e Ferramentas do Visual Studio para Contêineres](https://github.com/Microsoft/DockerTools)

