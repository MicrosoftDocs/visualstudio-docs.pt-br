---
title: Publicar no Serviço de Aplicativo do Azure
ms.custom: ''
ms.date: 06/22/2018
ms.technology: vs-ide-deployment
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- azure
ms.openlocfilehash: a8de7175b33a91c310da4b3d6d9e4c05c40c3522
ms.sourcegitcommit: 4f82c178b1ac585dcf13b515cc2a9cb547d5f949
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39341684"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio"></a>Publicar um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio

É possível usar a ferramenta **Publicar** para publicar aplicativos ASP.NET, ASP.NET Core, Node.js e .NET Core no Serviço de Aplicativo do Azure ou no Serviço de Aplicativo do Azure no Linux (usando contêineres). Para aplicativos Python, siga as etapas em [Python – Publicar no Serviço de Aplicativo do Azure](../python/publishing-python-web-applications-to-azure-from-visual-studio.md).

[!INCLUDE [quickstart-prereqs-azure](includes/quickstart-prereqs-azure.md)]

## <a name="publish-to-azure-app-service"></a>Publicar no Serviço de Aplicativo do Azure

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando Publicar no menu de contexto de projeto no Gerenciador de Soluções](../deployment/media/quickstart-publish.png "Escolha Publicar")

1. Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publica** será exibido; nesse caso, selecione **Criar novo perfil**.

1. Na caixa de diálogo **Escolher um destino de publicação**, escolha **Serviço de Aplicativo**.

    ![Escolher o Serviço de Aplicativo do Azure](../deployment/media/quickstart-publish-azure.png "Escolher o Serviço de Aplicativo do Azure")

1. Selecione **Publicar**. A caixa de diálogo **Criar Serviço de Aplicativo** é exibida. Entre com sua conta do Azure, se necessário, e as configurações padrão do serviço de aplicativo populam os campos.

    ![Criar o Serviço de Aplicativo](../deployment/media/quickstart-publish-settings-app-service.png "Criar o Serviço de Aplicativo do Azure")

1. Selecione **Criar**. O Visual Studio implanta o aplicativo em seu Serviço de Aplicativo do Azure e o aplicativo Web é carregado em seu navegador. O painel **Publicar** das propriedades do projeto mostra a URL e outros detalhes do site.

    ![Publicar painel de propriedade mostrando um resumo do perfil](../deployment/media/quickstart-publish-app-service-summary.png)

## <a name="clean-up-resources"></a>Limpar recursos

Nas etapas anteriores, você criou recursos do Azure em um grupo de recursos. Se você espera não precisar desses recursos no futuro, pode excluí-los excluindo o grupo de recursos.
No menu esquerdo no portal do Azure, selecione **Grupo de recursos** e, em seguida, selecione **myResourceGroup**.
Na página do grupo de recursos, certifique-se de que os recursos listados são aqueles que você deseja excluir.
Selecione **Excluir**, digite **myResourceGroup** na caixa de texto e, em seguida, selecione **Excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você aprendeu a usar o Visual Studio para criar um perfil de publicação para implantação no Azure. Também é possível configurar um perfil de publicação importando configurações de publicação do Serviço de Aplicativo do Azure.

> [!div class="nextstepaction"]
> [Importar configurações de publicação e implantar no Azure](tutorial-import-publish-settings-azure.md)
