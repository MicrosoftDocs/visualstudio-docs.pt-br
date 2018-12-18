---
title: Tour pelas funcionalidades de implantação
description: Saiba mais sobre as opções de implantação de aplicativos do Visual Studio.
ms.custom: mvc
ms.date: 06/22/2018
ms.technology: vs-ide-deployment
ms.topic: quickstart
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET applications, deploying
- components [Visual Studio], deploying
- installers
- publishing
- deploying applications [Visual Studio]
- deploying applications [Visual Studio], about deploying applications
- components [.NET Framework], deploying
ms.assetid: 63fcdd5b-2e54-4210-9038-65bc23167725
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 682010bc4235948918b3bffce70d04d5db0781af
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861625"
---
# <a name="quickstart-first-look-at-deployment-in-visual-studio"></a>Guia de Início Rápido: Introdução à implantação no Visual Studio

Ao implantar um aplicativo, serviço ou componente, você o distribui para instalação em outros computadores, dispositivos, servidores ou na nuvem. Você escolhe o método apropriado no Visual Studio para o tipo de implantação que deseja. (Muitos tipos de aplicativo são compatíveis com outras ferramentas de implantação como implantação de linha de comando ou o NuGet, as quais não são descritas aqui).

Confira os guias de Início Rápido e Tutoriais para obter instruções passo a passo de implantação. Para uma visão geral sobre as opções de implantação, confira [Quais opções de publicação são adequadas para mim?](deploying-applications-services-and-components-resources.md#what-publishing-options-are-right-for-me).

## <a name="deploy-to-local-folder"></a>Implantar na pasta local

A implantação em uma pasta local é normalmente usada para teste ou para iniciar uma implantação de teste em que outra ferramenta é usada para a implantação final.

- **ASP.NET**, **ASP.NET Core**, **Node.js**, **Python** e .**NET Core**: use a ferramenta Publicar para implantar em uma pasta local. As opções exatas disponíveis dependem do tipo de aplicativo. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar**. (Se você já tiver configurado algum perfil de publicação, será necessário clicar em **Criar novo perfil**). Em seguida, escolha **Pasta**. Para saber mais, confira [Implantar em uma pasta local](quickstart-deploy-to-local-folder.md).

    ![Escolha Publicar](../deployment/media/quickstart-publish.png)

- **Tempo de execução do Visual C++**: você pode implantar o tempo de execução do Visual C++ usando a implantação local ou a vinculação estática. Para obter mais informações, confira [Implantando aplicativos nativos da área de trabalho (Visual C++)](/cpp/ide/deploying-native-desktop-applications-visual-cpp).

## <a name="publish-to-azure"></a>Publicar no Azure

- **ASP.NET**, **ASP.NET Core**, **Python** e **Node.js**: você pode usar a ferramenta Publicar para implantar rapidamente aplicativos no Serviço de Aplicativo do Azure ou em uma Máquina Virtual do Azure. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione **Publicar**. (Se você já tiver configurado algum perfil de publicação, será necessário clicar em **Criar novo perfil**). Na caixa de diálogo Publicar, escolha **Serviço de Aplicativo** ou **Máquinas Virtuais do Azure** e, em seguida, siga as etapas de configuração.

    ![Escolher o Serviço de Aplicativo do Azure](../deployment/media/quickstart-publish-azure.png "Escolher o Serviço de Aplicativo do Azure")

    No Visual Studio 2017 versão 15.7 e posterior, você poderá implantar aplicativos ASP.NET Core no **Serviço de Aplicativo para Linux**.

    Para aplicativos do Python, confira também [Python – publicar no Serviço de Aplicativo do Azure](/visualstudio/python/publishing-python-web-applications-to-azure-from-visual-studio?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json).

    Para uma rápida introdução, confira [Publicar no Azure](quickstart-deploy-to-azure.md) e [Publicar no Linux](quickstart-deploy-to-linux.md). Confira também [Publicar um aplicativo ASP.NET Core no Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs). Para implantação usando o Git, confira [Implantação contínua do ASP.NET Core no Azure com o Git](/aspnet/core/publishing/azure-continuous-deployment).

    Para obter informações sobre como importar um perfil de publicação do Serviço de Aplicativo do Azure para o Visual Studio, confira [Importar configurações de publicação e implantar no Azure](../deployment/tutorial-import-publish-settings-azure.md).

    > [!NOTE]
    > Se você ainda não tem uma conta do Azure, pode [inscrever-se aqui](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=doc&utm_campaign=visualstudio).

## <a name="publish-to-web-or-deploy-to-network-share"></a>Publicar na Web ou implantar em compartilhamento de rede

- **ASP.NET**, **ASP.NET Core**, **Node.js** e **Python**: você pode usar a ferramenta Publicar para implantar em um site usando FTP ou Implantação da Web. Para obter mais informações, confira [Implantar um site da Web](quickstart-deploy-to-a-web-site.md).

    No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e selecione **Publicar**. (Se você já tiver configurado algum perfil de publicação, será necessário clicar em **Criar novo perfil**). Na ferramenta Publicar, escolha a opção desejada e siga as etapas de configuração.

    ![Escolha IIS, FTP, etc.](../deployment/media/quickstart-publish-iis-ftp.png)

    Para obter informações sobre como importar um perfil de publicação no Visual Studio, confira [Importar configurações de publicação e implantar no IIS](../deployment/tutorial-import-publish-settings-iis.md).

    Você também pode implantar aplicativos e serviços ASP.NET de várias outras maneiras. Para obter mais informações, confira [Implantando aplicativos e serviços Web ASP.NET](http://www.asp.net/aspnet/overview/deployment).

- **Tempo de execução do Visual C++**: você pode implantar o tempo de execução do Visual C++ usando a implantação central. Para obter mais informações, confira [Implantando aplicativos nativos da área de trabalho (Visual C++)](/cpp/ide/deploying-native-desktop-applications-visual-cpp).

- **Área de Trabalho do Windows** Você pode publicar um aplicativo de área de trabalho do Windows em um servidor Web ou em um compartilhamento de arquivo de rede usando a implantação ClickOnce. Os usuários podem, então, instalar o aplicativo com um único clique. Para obter mais informações, confira [Implantar um aplicativo da área de trabalho usando o ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) e [Implantar um aplicativo nativo usando o ClickOnce](/cpp/ide/clickonce-deployment-for-visual-cpp-applications).

## <a name="publish-to-microsoft-store"></a>Publicar na Microsoft Store

No Visual Studio, você pode criar pacotes de aplicativos para implantação na Microsoft Store.

- **UWP**: você pode empacotar o aplicativo e implantá-lo usando itens de menu. Para saber mais, confira [Empacotar um aplicativo UWP usando o Visual Studio](/windows/uwp/packaging/packaging-uwp-apps).

    ![Criar um pacote de aplicativos](../deployment/media/feature-tour-create-app-package.jpg)

- **Área de trabalho do Windows**: você pode implantar na Microsoft Store usando a Ponte de Desktop do Visual Studio 2017 versão 15.4 em diante. Para fazer isso, comece criando um Projeto de Empacotamento de Aplicativos do Windows. Para obter mais informações, confira [Empacotar um aplicativo da área de trabalho para a Microsoft Store (Ponte de Desktop)](/windows/uwp/porting/desktop-to-uwp-packaging-dot-net).

    ![Ponte de Desktop](../deployment/media/feature-tour-desktop-bridge.png)

## <a name="deploy-to-a-device-uwp"></a>Implantar em um dispositivo (UWP)

Se você estiver implantando um aplicativo UWP para testar em um dispositivo, confira [Executar aplicativos UWP em um computador remoto no Visual Studio](../debugger/run-windows-store-apps-on-a-remote-machine.md).

## <a name="create-an-installer-package-windows-client"></a>Criar um pacote de instalador (cliente do Windows)

Se precisa de uma instalação mais complexa de um aplicativo da área de trabalho do que o [ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) pode oferecer, você pode criar um pacote de instalador, um projeto de instalação ou um bootstrapper personalizado.

- Um instalador WiX baseado em MSI pode ser criado usando a [Extensão WiX Toolset do Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension).

- O [InstallShield](https://www.flexerasoftware.com/producer/products/software-installation/installshield-software-installer/tab/requirements) da Flexera Software pode ser usado com o Visual Studio 2017 (não compatível com a Community Edition). Observe que o InstallShield Limited Edition não está mais incluído no Visual Studio e não é compatível com o Visual Studio 2017: entre em contato com a [Flexera Software](http://learn.flexerasoftware.com/content/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio) para informações sobre a disponibilidade futura.

- Se você desejar criar um Projeto de instalação (vdproj), instale a [extensão de Projetos de instalador do Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.MicrosoftVisualStudio2017InstallerProjects#overview).

- Você pode instalar os componentes de pré-requisitos para aplicativos de área de trabalho configurando um instalador genérico, que é conhecido como bootstrapper. Para obter mais informações, confira [Pré-requisitos de Implantação de aplicativos](../deployment/application-deployment-prerequisites.md).

## <a name="deploy-to-test-lab"></a>Implantar em laboratório de teste

Você pode permitir desenvolvimento e testes mais sofisticados implantando seus aplicativos em ambientes virtuais. Para obter mais informações, confira [Testar em um ambiente de laboratório](../test/lab-management/using-a-lab-environment-for-your-application-lifecycle.md).

## <a name="devops-deployment"></a>Implantação de DevOps

Em um ambiente de equipe, você pode usar Azure Pipelines para permitir a implantação contínua do seu aplicativo. Para obter mais informações, confira [Azure Pipelines](/azure/devops/pipelines/index?view=vsts) e [Implantar no Azure](/azure/devops/deploy-azure/index?view=vsts).

## <a name="deployment-for-other-app-types"></a>Implantação de outros tipos de aplicativos

| Tipo de aplicativo | Cenário de implantação | Link |
| --- | --- | --- |
| **Aplicativo do Office** | Você pode publicar um suplemento do Office no Visual Studio. | [Implantar e publicar seu suplemento do Office](https://dev.office.com/docs/add-ins/publish/publish) |
| **Serviço WCF ou OData** | Outros aplicativos podem usar os serviços RIA WCF que você implanta em um servidor Web. | [Desenvolvendo e implantando WCF Data Services](/dotnet/framework/data/wcf/developing-and-deploying-wcf-data-services) |
| **LightSwitch** | O LightSwitch não é mais compatível com o Visual Studio 2017, mas ainda pode ser implantado no Visual Studio 2015 e anteriores. | [Implantando aplicativos LightSwitch](https://msdn.microsoft.com/Library/4818d933-295c-4ecc-9148-7ad9ca28dcdb) |

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você obteve uma visão geral das opções de implantação para diferentes aplicativos.

> [!div class="nextstepaction"]
> [Quais opções de publicação são adequadas para mim?](deploying-applications-services-and-components-resources.md#what-publishing-options-are-right-for-me)
