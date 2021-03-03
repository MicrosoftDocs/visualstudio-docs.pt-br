---
title: Ferramentas do Visual Studio para Docker com ASP.NET
author: ghogen
description: Saiba como usar as ferramentas e Docker for Windows do Visual Studio 2019
ms.author: ghogen
ms.date: 02/22/2021
ms.prod: visual-studio-dev16
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: 3a2c0d9ac31857fb2389455b0262373414981c5b
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751078"
---
Com o Visual Studio, você pode facilmente compilar, depurar e executar aplicativos em contêineres .NET, ASP.NET e ASP.NET Core e publicá-los no ACR (registro de contêiner do Azure), no Hub do Docker, no serviço de Azure App ou no seu próprio registro de contêiner. Neste artigo, publicaremos um aplicativo ASP.NET Core no ACR.

## <a name="prerequisites"></a>Pré-requisitos

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com **Desenvolvimento para a Web**, a carga de trabalho de **Ferramentas do Azure** e/ou **Desenvolvimento multiplataforma do .NET Core** instalados
* [Ferramentas de desenvolvimento do .NET Core](https://dotnet.microsoft.com/download/dotnet-core/) para desenvolvimento com o .NET Core
* Para publicar no Registro de Contêiner do Azure, uma assinatura do Azure. [Inscreva-se em uma avaliação gratuita](https://azure.microsoft.com/free/dotnet/).

## <a name="installation-and-setup"></a>Instalação e configuração

Para a instalação do Docker, primeiro examine as informações no [Docker desktop para Windows: o que saber antes de instalar](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)o. Em seguida, instale o [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

## <a name="add-a-project-to-a-docker-container"></a>Adicionar um projeto a um contêiner do Docker

1. Crie um novo projeto usando o modelo de **aplicativo web ASP.NET Core** ou se desejar usar o .NET Framework em vez do .NET Core, escolha **aplicativo web ASP.net (.NET Framework)**.
1. Na tela **informações adicionais** , verifique se a caixa de seleção **habilitar suporte ao Docker** está marcada.

   ![Caixa de seleção Habilitar Suporte do Docker](../../media/container-tools/vs-2019/webapp-additional-information-31-docker.png)

   A captura de tela mostra o .NET Core; Se você estiver usando .NET Framework, parecerá um pouco diferente.

1. Selecione o tipo de contêiner desejado (Windows ou Linux) e clique em **Criar**.

## <a name="dockerfile-overview"></a>Visão geral do Dockerfile

Um *Dockerfile*, ou seja, a receita para criar uma imagem final do Docker, é criado no projeto. Confira a [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para entender os comandos que ele contém:

```dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1903 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-nanoserver-1903 AS build
WORKDIR /src
COPY ["WebApplication1/WebApplication1.csproj", "WebApplication1/"]
RUN dotnet restore "WebApplication1/WebApplication1.csproj"
COPY . .
WORKDIR "/src/WebApplication1"
RUN dotnet build "WebApplication1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication1.dll"]
```

O *Dockerfile* anterior baseia-se na imagem [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) e inclui instruções para modificar a imagem base criando o projeto e adicionando-o ao contêiner. Se você estiver usando a .NET Framework, a imagem base será diferente.

Quando a caixa de seleção **Configurar para HTTPS** do novo projeto estiver marcada, o *Dockerfile* exibirá duas portas. Uma porta é usada para o tráfego HTTP; a outra porta é usada para o HTTPS. Se a caixa de seleção não estiver marcada, uma única porta (80) será exposta para o tráfego HTTP.

## <a name="debug"></a>Depurar

Selecione **Docker** no menu suspenso de depuração na barra de ferramentas e inicie a depuração do aplicativo. Poderá aparecer uma mensagem com um aviso sobre a confiança em um certificado, escolha confiar no certificado para continuar.

A opção **Ferramentas de Contêiner** na janela **Saída** mostra quais ações estão ocorrendo. Na primeira vez, pode levar algum tempo para baixar a imagem base, mas é muito mais rápido em execuções subsequentes.

>[!NOTE]
> Se você precisar alterar as portas para depuração, poderá fazer isso na *launchSettings.jsno* arquivo. Consulte [configurações de inicialização do contêiner](../../container-launch-settings.md).

## <a name="containers-window"></a>Janela contêineres

Se você tiver o Visual Studio 2019 versão 16,4 ou posterior, poderá usar a janela **contêineres** para exibir contêineres em execução em seu computador, bem como imagens disponíveis.

Abra a janela **contêineres** usando a caixa de pesquisa no IDE (pressione **Ctrl** + **Q** para usá-la), digite `container` e escolha a janela **contêineres** na lista.

Você pode montar a janela **contêineres** em um local conveniente, como abaixo do editor, movendo-a e seguindo os guias de posicionamento da janela.

Na janela, localize o contêiner e percorra cada guia para exibir as variáveis de ambiente, os mapeamentos de porta, os logs e o sistema de arquivos.

![Captura de tela da janela contêineres](../../media/overview/vs-2019/container-tools-window.png)

Para obter mais informações, consulte [Exibir e diagnosticar contêineres e imagens no Visual Studio](../../view-and-diagnose-containers.md).

## <a name="publish-docker-images"></a>Publicar imagens do Docker

Depois que o ciclo de desenvolvimento e de depuração do aplicativo forem concluídos, você poderá criar uma imagem de produção do aplicativo.

1. Altere a lista suspensa de configuração para **Versão** e compile o aplicativo.
1. Clique com o botão direito no projeto em **Gerenciador de Soluções** e escolha **Publicar**.
1. Na caixa de diálogo **publicar** , selecione a guia **registro de contêiner do Docker** .

   ![Captura de tela da caixa de diálogo de publicação – escolha registro de contêiner do Docker](../../media/container-tools/vs-2019/docker-container-registry.png)

1. Escolha **criar novo registro de contêiner do Azure**.

   ![Captura de tela da caixa de diálogo de publicação – escolha criar um novo registro de contêiner do Azure](../../media/container-tools/vs-2019/select-existing-or-create-new-azure-container-registry.png)

1. Preencha os valores desejados em **Criar um novo Registro de Contêiner do Azure**.

    | Configuração      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Prefixo DNS** | Nome globalmente exclusivo | Nome que identifica exclusivamente o registro de contêiner. |
    | **Assinatura** | Escolha sua assinatura | A assinatura do Azure a utilizar. |
    | **[Grupo de Recursos](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  Nome do grupo de recursos no qual criar o registro de contêiner. Escolha **Novo** para criar um novo grupo de recursos.|
    | **[SKU](/azure/container-registry/container-registry-skus)** | Standard | Camada de serviço do registro de contêiner  |
    | **Local do Registro** | Um local próximo | Escolha um Local em uma [região](https://azure.microsoft.com/regions/) próxima a você ou perto de outros serviços que usarão o registro de contêiner. |

    ![Caixa de diálogo Criar um Registro de Contêiner do Azure do Visual Studio][0]

1. Clique em **Criar**. A caixa de diálogo **publicar** agora mostra o registro criado.

   ![Captura de tela da caixa de diálogo Publicar mostrando o registro de contêiner do Azure criado](../../media/container-tools/vs-2019/created-azure-container-registry.png)

1. Escolha **concluir** para concluir o processo de publicação da imagem de contêiner no registro recém-criado no Azure.

   ![Captura de tela mostrando a publicação bem-sucedida](../../media/container-tools/vs-2019/publish-succeeded.png)

## <a name="next-steps"></a>Próximas etapas

Agora, é possível extrair o contêiner do registro para qualquer host capaz de executar imagens do Docker, por exemplo [Instâncias de Contêiner do Azure](/azure/container-instances/container-instances-tutorial-deploy-app).

[0]:../../media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog-2019.png
