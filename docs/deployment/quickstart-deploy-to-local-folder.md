---
title: Implantar em uma pasta local
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bcf17504f5ae057e68544d26e071bb74cc7b83bf
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263532"
---
# <a name="deploy-an-app-to-a-local-folder-using-visual-studio"></a>Implantar um aplicativo em uma pasta local usando o Visual Studio

É possível usar a ferramenta **Publicar** para publicar aplicativos ASP.NET, ASP.NET Core, .NET Core e Python em uma pasta local do Visual Studio. Para Node.js, há suporte para as etapas, mas a interface do usuário é diferente.

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> Se você precisar publicar um aplicativo da área de trabalho do Windows em uma pasta local, confira [Implantar um aplicativo da área de trabalho usando o ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) (C# ou Visual Basic). Para C++/CLR, confira [Implantar um aplicativo nativo usando o ClickOnce](/cpp/windows/clickonce-deployment-for-visual-cpp-applications) ou, para C/C++, confira [Implantar um aplicativo nativo usando um projeto de instalação](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project).

## <a name="deploy-to-a-local-folder"></a>Implantar em uma pasta local

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando Publicar no menu de contexto de projeto no Gerenciador de Soluções](../deployment/media/quickstart-publish.png "Escolha Publicar")

1. Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Selecione **Criar novo perfil**.

1. Na caixa de diálogo **Escolher um destino de publicação**, escolha **Pasta**.

    ![Escolher pasta local como um destino de publicação](../deployment/media/quickstart-publish-folder.png "Escolher pasta")

1. Insira um caminho ou selecione **Procurar** para especificar uma pasta local.

1. Selecione **Publicar**. O Visual Studio cria o projeto e o publica na pasta especificada. O painel **Publicar** das propriedades do projeto é exibido, mostrando um resumo do perfil.

    ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-publish-folder-summary.png)

1. Para definir as configurações de implantação, selecione **Configurar** no resumo do perfil e selecione a guia **Configurações**.

    ![Configurações de perfil](../deployment/media/quickstart-profile-settings.png "Configurações de perfil")

1. Configure opções como se deseja implantar uma configuração de depuração ou de versão e, em seguida, selecione **Salvar**.

1. Para republicar, selecione **Publicar**.

Implante os arquivos publicados na maneira que desejar. Por exemplo, é possível empacotá-los em um arquivo *.zip*, usar um simples comando para copiar ou implantá-los com qualquer pacote de instalação de sua escolha.

## <a name="next-steps"></a>Próximas etapas

- [Implantar um aplicativo do .NET Core com a ferramenta Publicar](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Empacotar um aplicativo da área de trabalho para a Microsoft Store (Ponte de Desktop)](/windows/uwp/porting/desktop-to-uwp-packaging-dot-net?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- (.NET) [Implantar o .NET Framework e aplicativos](/dotnet/framework/deployment/)
