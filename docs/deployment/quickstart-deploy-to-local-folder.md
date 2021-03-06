---
title: Implantar em uma pasta local
description: Saiba como usar a ferramenta de publicação para publicar aplicativos ASP.NET, ASP.NET Core, .NET Core e Python em uma pasta do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 23ef2036af7b93ee6eeaaa14cb8733a4e0ced638
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249496"
---
# <a name="deploy-an-app-to-a-folder-using-visual-studio"></a>Implantar um aplicativo em uma pasta usando o Visual Studio

Você pode usar a ferramenta de **publicação** para publicar aplicativos ASP.NET, ASP.NET Core, .NET Core e Python em uma pasta do Visual Studio. Para Node.js, há suporte para as etapas, mas a interface do usuário é diferente.

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]
::: moniker range=">=vs-2017"
> [!NOTE]
> Se você precisar publicar um aplicativo de área de trabalho do Windows em uma pasta, consulte [implantar um aplicativo de área de trabalho usando o ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) (C# ou Visual Basic). Para C++/CLR, confira [Implantar um aplicativo nativo usando o ClickOnce](/cpp/windows/clickonce-deployment-for-visual-cpp-applications) ou, para C/C++, confira [Implantar um aplicativo nativo usando um projeto de instalação](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project).

::: moniker-end

::: moniker range=">=vs-2019"
> [!NOTE]
> Se você precisar publicar um aplicativo de área de trabalho do Windows .NET Core 3,1 ou mais recente em uma pasta, consulte [implantar um aplicativo .net do Windows usando o ClickOnce](quickstart-deploy-using-clickonce-folder.md).

::: moniker-end

## <a name="deploy-to-a-local-folder"></a>Implantar em uma pasta local

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando publicar no menu de contexto do projeto no Gerenciador de Soluções](../deployment/media/quickstart-publish.png "Escolha Publicar")

1. Se você tiver configurado anteriormente todos os perfis de publicação, a janela **publicar** será exibida. Selecione **Novo**.

1. Na janela **publicar** , selecione **pasta**.

   ![Escolher pasta como um destino de publicação](../deployment/media/quickstart-publish-folder-new.png "Escolher pasta")

   ::: moniker range=">=vs-2019"

   Se você estiver implantando um aplicativo do Windows .NET Core 3,1 ou mais recente, talvez seja necessário selecionar a **pasta** na janela de **destino específica** .

   ![Escolher pasta como destino específico](../deployment/media/quickstart-publish-folder-targets.png "Escolher destino específico")

   Se você quiser publicar um aplicativo do Windows .NET Core 3,1 ou mais recente com o ClickOnce, consulte [implantar um aplicativo .net do Windows usando o ClickOnce](quickstart-deploy-using-clickonce-folder.md).
   ::: moniker-end

1. Insira um caminho ou selecione **procurar** para especificar uma pasta.

   ![Especifique o caminho para a pasta](../deployment/media/quickstart-publish-folder-path.png "Escolher pasta")

   ::: moniker range=">=vs-2019"
   Clique em **concluir** para salvar o perfil.

   ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. Selecione **Publicar**. O Visual Studio cria o projeto e o publica na pasta especificada.

   ::: moniker range="vs-2017"
   O painel **Publicar** das propriedades do projeto é exibido, mostrando um resumo do perfil.

   ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. Para definir as configurações de implantação, selecione **Editar** no resumo do perfil de publicação e selecione a guia **configurações** .

   As configurações que você vê dependem do seu tipo de aplicativo. A ilustração a seguir mostra as configurações de exemplo para um aplicativo ASP.NET Core.

    ![Configurações de perfil](../deployment/media/quickstart-profile-settings.png "Configurações de perfil")

    Para obter ajuda adicional para escolher as configurações no .NET, consulte o seguinte:

    - [Implantação dependente da estrutura vs. autônoma](/dotnet/core/deploying/)
    - [Identificadores de tempo de execução de destino (RID portátil, et al)](/dotnet/core/rid-catalog)
    - [Configurações de depuração e versão](../ide/understanding-build-configurations.md)

1. Configure opções como se deseja implantar uma configuração de depuração ou de versão e, em seguida, selecione **Salvar**.

1. Para republicar, selecione **Publicar**.

Implante os arquivos publicados na maneira que desejar. Por exemplo, é possível empacotá-los em um arquivo *.zip*, usar um simples comando para copiar ou implantá-los com qualquer pacote de instalação de sua escolha.

## <a name="next-steps"></a>Próximas etapas

Para aplicativos .NET:

- [Implantar um aplicativo .NET Core com a ferramenta de publicação](/dotnet/core/deploying/deploy-with-vs)
- [Publicação de aplicativos do .NET Core (implantações dependentes da estrutura vs. independentes)](/dotnet/core/deploying/)
- [Implantar o .NET Framework e os aplicativos](/dotnet/framework/deployment/)
::: moniker range=">=vs-2019"
- [Implante um aplicativo .net do Windows usando o ClickOnce](quickstart-deploy-using-clickonce-folder.md).
 ::: moniker-end
