---
title: Publicar no Serviço de Aplicativo do Azure
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- azure
ms.openlocfilehash: 19eca9747fa4e9ef80f7de05799a2cee685ce821
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285516"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio"></a>Publicar um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio

Para aplicativos ASP.NET, ASP.NET Core, Node.js e .NET Core, publique no Serviço de Aplicativo do Azure ou no Serviço de Aplicativo do Azure no Linux (usando contêineres) usando um dos métodos a seguir.

* Para implantação contínua (ou automática) de aplicativos, use o Azure DevOps com [Azure Pipelines](/azure/devops/pipelines/get-started-yaml?view=azdevops).

* Para implantação única (ou manual) de aplicativos, use a ferramenta **Publicar** no Visual Studio para implantar aplicativos ASP.NET, ASP.NET Core, Node.js e .NET Core no Serviço de Aplicativo do Azure ou Serviço de Aplicativo para Linux (usando contêineres). Para aplicativos Python, siga as etapas em [Python – Publicar no Serviço de Aplicativo do Azure](../python/publishing-python-web-applications-to-azure-from-visual-studio.md).

Este artigo descreve como usar a ferramenta **Publicar** para uma implantação única.

[!INCLUDE [quickstart-prereqs-azure](includes/quickstart-prereqs-azure.md)]

## <a name="publish-to-azure-app-service-on-windows"></a>Publicar no serviço de Azure App no Windows

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando publicar no menu de contexto do projeto no Gerenciador de Soluções](../deployment/media/quickstart-publish.png "Escolha Publicar")

1. Na caixa de diálogo **publicar** , selecione **Azure**.

    ![Escolher destino de publicação](../deployment/media/quickstart-publish-azure-new.png)

1. Selecione * * serviço de Azure App (Windows) * * e **Avançar**.

    ![Escolha o serviço de Azure App no Linux](../deployment/media/quickstart-publish-windows-select-azure-service.png)

1. Entre com sua conta do Azure, se necessário. Selecione **criar um novo serviço de Azure app...**

    ![Link para criar uma nova instância do serviço de Azure App](../deployment/media/quickstart-publish-windows-create-new-link.png)

1. Na caixa de diálogo **criar Azure app serviço (Windows)** , os campos **nome do aplicativo**, **grupo de recursos**e entrada do plano do **serviço de aplicativo** são preenchidos. Você pode manter esses nomes ou alterá-los. Quando estiver pronto, selecione **criar**.

    ![Escolher serviço de Azure App](../deployment/media/quickstart-publish-windows-create-new-dialog.png)

1. Na caixa de diálogo **publicar** , a instância recém-criada foi selecionada automaticamente. Quando estiver pronto, clique em **concluir**.

    ![Escolher serviço de Azure App](../deployment/media/quickstart-publish-windows-select-instance.png)

1. Selecione **Publicar**. O Visual Studio implanta o aplicativo em seu Serviço de Aplicativo do Azure e o aplicativo Web é carregado em seu navegador. O painel **Publicar** das propriedades do projeto mostra a URL e outros detalhes do site.

    ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-publish-windows-summary-page.png)

## <a name="clean-up-resources"></a>Limpar os recursos

Nas etapas anteriores, você criou os recursos do Azure em um grupo de recursos. Se você não espera precisar desses recursos no futuro, poderá excluí-los ao excluir o grupo de recursos.
No menu à esquerda no portal do Azure, selecione **Grupos de recursos** e, em seguida, selecione **myResourceGroup**.
Na página do grupo de recursos, certifique-se de que os recursos listados são aqueles que deseja excluir.
Selecione **Excluir**, digite **myResourceGroup** na caixa de texto e selecione **Excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você aprendeu a usar o Visual Studio para criar um perfil de publicação para implantação no Azure. Também é possível configurar um perfil de publicação importando configurações de publicação do Serviço de Aplicativo do Azure.

> [!div class="nextstepaction"]
> [Importar configurações de publicação e implantar no Azure](tutorial-import-publish-settings-azure.md)
