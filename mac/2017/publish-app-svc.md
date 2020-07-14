---
title: Publicar no Serviço de Aplicativo do Azure
ms.date: 01/17/2019
helpviewer_keywords:
- deployment, website
ms.assetid: 8524a4c5-97a9-41ac-a2a0-034efb9bfc57
author: sayedihashimi
ms.author: sayedha
manager: unniravindranathan
ms.prod: visual-studio-mac
ms.custom: video
ms.topic: how-to
ms.workload:
- azure
ms.openlocfilehash: 42f455c824697e0909c990932611bb440a23a2af
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950442"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio-for-mac"></a>Publicar um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio para Mac

Você pode usar a ferramenta Publicar para publicar aplicativos do ASP.NET Core no Serviço de Aplicativo do Azure.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2017 para Mac](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs4mac2017) instalado com o ASP.NET Core habilitado.
- Uma assinatura do Azure. Se você ainda não tiver uma assinatura, [Inscreva-se gratuitamente](https://azure.microsoft.com/free/dotnet/), ganhando US$ 200 em créditos para 30 dias e 12 meses de serviços populares gratuitos.
- Um projeto ASP.NET Core. Se você ainda não tiver um projeto, [crie um](/visualstudio/mac/create-new-projects?view=vsmac-2017).

## <a name="publish-to-azure-app-service"></a>Publicar no Serviço de Aplicativo do Azure

 1. No Painel de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar**.

    ![Menu de contexto Publicar](media/publish-context-menu.png)

 2. Se você já tiver publicado este projeto no Serviço de Aplicativo do Azure, o perfil de publicação será exibido no menu. Selecione o perfil de publicação para iniciar o processo de publicação.

 3. Para publicar esse projeto no Serviço de Aplicativo pela primeira vez, selecione **Publicar no Azure**

    ![Menu de contexto Publicar no Serviço de Aplicativo](media/publish-to-azure-context-menu.png)

 4. A caixa de diálogo **Publicar no Serviço de Aplicativo do Azure** aparece, e os Serviços de Aplicativos existentes são mostrados. Para publicar em um Serviço de Aplicativo existente, selecione o Serviço de Aplicativo na lista e, em seguida, clique em **Publicar**.

    ![Caixa de diálogo Publicar no Serviço de Aplicativo do Azure](media/publish-to-app-service-dialog.png)

 5. Para criar um Serviço de Aplicativo, clique no botão **Novo**.

    ![Caixa de diálogo Publicar no Serviço de Aplicativo](media/publish-to-app-service-dialog-new-selected.png)

 6. A caixa de diálogo **Novo Serviço de Aplicativo** é exibida. Nesta caixa de diálogo, você pode definir as configurações do novo Serviço de Aplicativo.

    ![Caixa de diálogo Novo Serviço de Aplicativo](media/publish-new-app-service.png)

    Há algumas opções de personalização a serem consideradas aqui. O nome do Serviço de Aplicativo será assumido como o nome do projeto. Se o nome não estiver disponível, um sinal de aviso será exibido no lado direito do campo de entrada. O nome do Serviço de Aplicativo será usado na URL do site, portanto, o nome precisa ser válido para ser usado em uma URL.

    Você pode alterar a assinatura à qual o Serviço de Aplicativo será associado usando a lista suspensa **Assinatura**.

    Você pode selecionar um **Grupo de Recursos** existente usando o menu suspenso ou criar outro com o botão **+**.

    Para o Plano do Serviço de Aplicativo, selecione um existente ou crie outro selecionando o botão de opção **Personalizado**.

    Para criar seu Serviço de Aplicativo e publicar o projeto nele, clique em **Criar**.

    Depois que você clicar em **Criar**, a caixa de diálogo **Novo Serviço de Aplicativo** será ignorada e a seguinte mensagem será exibida indicando que a criação do Serviço de Aplicativo foi iniciada.

      ![Mensagem de criação do Serviço de Aplicativo](media/publish-create-app-service-message.png)

    Depois que você clicar em **OK**, a mensagem será descartada e você poderá continuar trabalhando no projeto. Você pode observar o status do processo de publicação com a barra de status na parte superior do IDE. Depois que o aplicativo Web for publicado com êxito, o site será aberto com o navegador padrão.

## <a name="related-video"></a>Vídeo relacionados

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Publish-to-Azure/player]
