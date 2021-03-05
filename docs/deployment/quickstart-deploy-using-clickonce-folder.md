---
description: A partir do Visual Studio 2019 versão 16,8, você pode usar a ferramenta de publicação para publicar aplicativos do .NET Core 3,1 ou mais recentes do Windows desktop usando o ClickOnce do Visual Studio.
title: Implantar um aplicativo de área de trabalho do Windows .NET usando o ClickOnce
ms.date: 10/15/2020
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder, ClickOnce
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: john-hart
ms.author: JohnHart
manager: jmartens
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: d3977408f191aabc734226fd6b637fcfaaf5e9de
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165703"
---
# <a name="deploy-a-net-windows-desktop-application-using-clickonce"></a>Implantar um aplicativo de área de trabalho do Windows .NET usando o ClickOnce

A partir do Visual Studio 2019 versão 16,8, você pode usar a ferramenta de **publicação** para publicar aplicativos do .net Core 3,1 ou mais recentes do Windows desktop usando o ClickOnce do Visual Studio.

> [!NOTE]
> Se você precisar publicar um .NET Framework aplicativo do Windows, consulte [implantar um aplicativo de área de trabalho usando o ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) (C# ou Visual Basic).

## <a name="publishing-with-clickonce"></a>Publicando com o ClickOnce

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando publicar no menu de contexto do projeto no Gerenciador de Soluções](../deployment/media/quickstart-clickonce-solution-explorer.png "Escolha Publicar")

1. Se você tiver configurado anteriormente todos os perfis de publicação, a página **publicar** será exibida. Selecione **Novo**.

1. No assistente de **publicação** , selecione **pasta**.

    ![Escolher pasta como um destino de publicação](../deployment/media/quickstart-clickonce-publish-folder-category.png "Escolher pasta")

1. Na página **destino específico** , selecione **ClickOnce**.

    ![Selecionar ClickOnce como o destino específico](../deployment/media/quickstart-clickonce-publish-folder-target.png "Escolher ClickOnce")

1. Insira um caminho ou selecione **procurar** para selecionar o local de publicação.

    ![Especifique o caminho para o local de publicação](../deployment/media/quickstart-clickonce-publish-location.png "Insira um caminho")

1. Na página **local de instalação** , selecione o local do qual os usuários instalarão o aplicativo.

    ![Especifique o caminho para a pasta](../deployment/media/quickstart-clickonce-install-location.png "Escolha o local de instalação")

1. Na página **configurações** , você pode fornecer as configurações necessárias para o ClickOnce.

1. Se você tiver selecionado para instalar a partir de um caminho UNC ou site, essa página permitirá que você especifique se o aplicativo está disponível offline. Quando selecionada, essa opção listará o aplicativo no menu iniciar dos usuários e permitirá que o aplicativo seja atualizado automaticamente quando uma nova versão for publicada. Por padrão, as atualizações estão disponíveis no local de instalação.  Se desejar ter um local diferente para as atualizações, você poderá especificar que usando o link configurações de atualização. Se você não quiser que o aplicativo fique disponível offline, ele será executado a partir do local de instalação.

    ![Especificar as configurações de publicação](../deployment/media/quickstart-clickonce-unc-settings.png "Escolher as configurações de publicação")

1. Se você tiver selecionado para instalar a partir de um CD, DVD ou unidade USB, essa página também permitirá que você especifique se o aplicativo oferece suporte a atualizações automáticas. Se você optar por dar suporte a atualizações, o local de atualização será necessário e deverá ser um caminho UNC ou um site válido.

    ![Escolher as configurações de publicação](../deployment/media/quickstart-clickonce-settings.png "Escolher as configurações de publicação")

Incluído nesta página está a capacidade de especificar quais **arquivos de aplicativo** serão incluídos na configuração, que os **pré-requisitos** de pacotes serão instalados e outras **Opções** por meio dos links na parte superior da página.

Também nesta página, você também pode definir a versão de publicação e se a versão for incrementada automaticamente com cada publicação.

> [!NOTE]
> O número de versão de publicação é exclusivo para cada perfil do ClickOnce. Se você planeja ter mais de um perfil, precisará ter isso em mente.

10. Na página **assinar manifestos** , você pode especificar se os manifestos devem ser assinados e qual certificado usar.

    ![Assinar os manifestos ClickOnce](../deployment/media/quickstart-clickonce-sign-manifests.png)

1. Na página **configuração** , você pode selecionar a configuração de projeto desejada.

     ![Especificar a configuração de publicação](../deployment/media/quickstart-clickonce-configuration.png)

    Para obter ajuda adicional sobre qual configuração escolher, consulte o seguinte:

    - [Implantação dependente da estrutura vs. autônoma](/dotnet/core/deploying/)
    - [Identificadores de tempo de execução de destino (RID portátil, et al)](/dotnet/core/rid-catalog)
    - [Configurações de depuração e versão](../ide/understanding-build-configurations.md)

1. Selecione **concluir** para salvar o novo perfil de publicação do ClickOnce.

1. Na página **Resumo** , selecione **publicar** e o Visual Studio cria o projeto e o publica na pasta de publicação especificada. Esta página também mostra um resumo do perfil.

    ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-clickonce-summary.png)

1. Para republicar, selecione **Publicar**.

## <a name="next-steps"></a>Próximas etapas

Para aplicativos .NET:

- [Implantar o .NET Framework e os aplicativos](/dotnet/framework/deployment/)
- [Referência do ClickOnce](clickonce-reference.md)
