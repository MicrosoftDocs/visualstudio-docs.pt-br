---
title: Publicar no Azure com a importação de configurações de publicação
ms.description: Create and import a publishing profile to deploy an application from Visual Studio to Azure App Service
ms.date: 05/07/2018
ms.technology: vs-ide-deployment
ms.topic: tutorial
helpviewer_keywords:
- deployment, publish settings
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2b4b0e4ea963f20199267f32a8c87440c8cc350b
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38808315"
---
# <a name="publish-an-application-to-azure-app-service-by-importing-publish-settings-in-visual-studio"></a>Publicar um aplicativo no Serviço de Aplicativo do Azure com a importação de configurações de publicação no Visual Studio

É possível usar a ferramenta **Publicar** para importar configurações de publicação e, em seguida, implantar seu aplicativo. Neste artigo, usamos configurações de publicação para o Serviço de Aplicativo do Azure, mas é possível usar etapas semelhantes para importar configurações de publicação do [IIS](../deployment/tutorial-import-publish-settings-iis.md). Em alguns cenários, o uso de um perfil de configurações de publicação pode ser mais rápido do que configurar manualmente a implantação no serviço para cada instalação do Visual Studio.

Essas etapas se aplicam a aplicativos ASP.NET, ASP.NET Core e .NET Core no Visual Studio. Também é possível importar as configurações de publicação de aplicativos [Python](../python/publishing-python-web-applications-to-azure-from-visual-studio.md). As etapas correspondem ao Visual Studio 2017 versão 15.6.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Gerar um arquivo de configurações de publicação do Serviço de Aplicativo do Azure
> * Importar o arquivo de configurações de publicação para o Visual Studio
> * Implantar o aplicativo no Serviço de Aplicativo do Azure

Um arquivo de configurações de publicação (*\*.publishsettings*) é diferente de um perfil de publicação (*\*.pubxml*) criado no Visual Studio. Um arquivo de configurações de publicação é criado pelo Serviço de Aplicativo do Azure e, em seguida, pode ser importado para o Visual Studio.

> [!NOTE]
> Se você precisar copiar um perfil de publicação do Visual Studio (arquivo *\*.pubxml*) de uma instalação do Visual Studio para outra, será possível encontrar o perfil de publicação, *\<nomedoperfil\>.pubxml*, na pasta *\\<nomedoprojeto\>\Properties\PublishProfiles* para tipos de projeto gerenciados. Para sites, examine embaixo da pasta *\App_Data*. Os perfis de publicação são arquivos XML do MSBuild.

## <a name="prerequisites"></a>Pré-requisitos

* É necessário ter o Visual Studio 2017 instalado e a carga de trabalho de desenvolvimento do **ASP.NET** e do .**NET Framework**. Para um aplicativo .NET Core, você também precisa da carga de trabalho do .**NET Core**.

    Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

* Crie um Serviço de Aplicativo do Azure. Para obter instruções detalhadas, confira [Implantar um aplicativo Web do ASP.NET Core no Azure usando o Visual Studio](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs).

## <a name="create-a-new-aspnet-project-in-visual-studio"></a>Criar um novo projeto ASP.NET no Visual Studio

1. No computador que executa o Visual Studio, escolha **Arquivo** > **Novo projeto**.

1. Em **Visual C#** ou **Visual Basic**, escolha **Web** e, em seguida, no painel do meio, escolha **Aplicativo Web ASP.NET (.NET Framework)** ou (apenas C#) **Aplicativo Web ASP.NET Core** e, em seguida, clique em **OK**.

    Se os modelos de projeto especificados não forem exibidos, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Confira os pré-requisitos neste artigo para identificar as cargas de trabalho do Visual Studio necessárias, que você deve instalar.

1. Escolha **MVC** (.NET Framework) ou **Aplicativo Web (Model-View-Controller)** (para .NET Core) e certifique-se de que **Sem autenticação** esteja selecionado. Em seguida, clique em **OK**.

1. Digite um nome como **MyWebApp** e clique em **OK**.

    O Visual Studio cria o projeto.

1. Escolha **Criar** > **Criar solução** para criar o projeto.

## <a name="create-the-publish-settings-file-in-azure-app-service"></a>Criar um arquivo de configurações de publicação no Serviço de Aplicativo do Azure

1. No portal do Azure, abra o Serviço de Aplicativo do Azure.

1. Clique em **Obter perfil de publicação** e salve o perfil localmente.

    ![Obter o perfil de publicação](../deployment/media/tutorial-azure-app-service-get-publish-profile.png)

    Um arquivo com uma extensão *.publishsettings* foi gerado na localização em que ele foi salvo. O código a seguir mostra um exemplo parcial do arquivo (em uma formatação mais legível).

    ```xml
    <publishData>
      <publishProfile
        profileName="DeployASPDotNetCore - Web Deploy"
        publishMethod="MSDeploy"
        publishUrl="deployaspdotnetcore.scm.azurewebsites.net:443"
        msdeploySite="DeployASPDotNetCore"
        userName="$DeployASPDotNetCore"
        userPWD="abcdefghijklmnopqrstuzwxyz"
        destinationAppUrl="http://deployaspdotnetcore20180508031824.azurewebsites.net"
        SQLServerDBConnectionString=""
        mySQLDBConnectionString=""
        hostingProviderForumLink=""
        controlPanelLink="http://windows.azure.com"
        webSystem="WebSites">
        <databases />
      </publishProfile>
    </publishData>
    ```
    Normalmente, o arquivo *.publishsettings anterior contém dois perfis de publicação que você pode usar no Visual Studio, uma para implantar usando a Implantação da Web e outro para implantar usando o FTP. O código anterior mostra o perfil de Implantação da Web. Os dois perfis serão importados posteriormente quando você importar o perfil.

## <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Importar as configurações de publicação no Visual Studio e implantar

[!INCLUDE [import publish settings](../deployment/includes/import-publish-settings-vs.md)]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um arquivo de configurações de publicação, importou-o para o Visual Studio e implantou um aplicativo ASP.NET no Serviço de Aplicativo do Azure. Talvez você queira ter uma visão geral das opções de publicação no Visual Studio.

> [!div class="nextstepaction"]
> [Introdução à implantação](../deployment/deploying-applications-services-and-components.md)
