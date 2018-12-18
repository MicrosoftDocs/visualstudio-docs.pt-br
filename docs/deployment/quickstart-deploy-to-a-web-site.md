---
title: Publicar em um site
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
- multiple
ms.openlocfilehash: 036d7549995f79808142c3a0a64e7e5f2075df2c
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39077497"
---
# <a name="publish-a-web-app-to-a-web-site-using-visual-studio"></a>Publique um aplicativo Web em um site usando o Visual Studio

É possível usar a ferramenta **Publicar** para publicar aplicativos ASP.NET, ASP.NET Core, .NET Core e Python em um site do Visual Studio. Para Node.js, há suporte para as etapas, mas a interface do usuário é diferente.

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

## <a name="publish-to-a-web-site"></a>Publicar em um site

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar** (ou use o item de menu **Criar** > **Publicar**).

    ![O comando Publicar no menu de contexto de projeto no Gerenciador de Soluções](../deployment/media/quickstart-publish.png "Escolha Publicar")

1. Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Selecione **Criar novo perfil**.

1. Na caixa de diálogo **Escolher um destino de publicação**, escolha **IIS, FTP, etc**.

    ![Escolher IIS, FTP, etc.](../deployment/media/quickstart-publish-iis-ftp.png "Escolher IIS, FTP, etc.")

1. Selecione **Publicar**. A caixa de diálogo de configurações de publicação do perfil é aberta.

    ![Escolher pasta](../deployment/media/quickstart-publish-settings-web.png "Escolher pasta")

1. No campo **Método de publicação**, escolha um método como **Implantação da Web** ou **FTP**. As configurações que você vir a seguir correspondem a seu método de publicação. A Implantação da Web simplifica a implantação de aplicativos Web e sites para servidores do IIS e precisa ser instalada como um aplicativo no servidor. Use o [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) para instalá-la.

1. Defina as configurações necessárias para o método de publicação e selecione **Validar conexão**. Se o servidor ou o destino estiver disponível e as configurações estiverem corretas, uma mensagem que indica a conexão será validada e você estará pronto para publicar.

    ![Validar sua conexão](../deployment/media/quickstart-publish-web-deploy.png "Validar sua conexão")

1. Selecione **Configurações** para definir outras configurações de implantação, como se deseja implantar uma configuração de depuração ou de versão e, em seguida, selecione **Salvar**. Se você estiver depurando remotamente, será necessária uma configuração de depuração.

1. Para publicar, selecione **Publicar**. A janela de Saída mostra o progresso da implantação e os resultados.

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você aprendeu a usar o Visual Studio para criar um perfil de publicação. Também é possível configurar um perfil de publicação importando as configurações de publicação.

> [!div class="nextstepaction"]
> [Importar configurações de publicação e implantar no IIS](tutorial-import-publish-settings-iis.md)
