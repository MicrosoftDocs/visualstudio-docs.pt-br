---
title: Acessando nuvens privadas do Azure
description: Saiba como acessar recursos de nuvem privada usando o Visual Studio.
author: ghogen
manager: jillfra
assetId: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/13/2017
ms.author: ghogen
ms.openlocfilehash: 6c1b46e34c688f232ee1f774ff2d19fdad7ff6bf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280382"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Acessando nuvens privadas do Azure com o Visual Studio

Por padrão, o Visual Studio dá suporte a pontos de extremidade REST de nuvem do Azure. Neste artigo, você aprende a usar o certificado da nuvem privada para acessar e interagir com a nuvem privada no Visual Studio.

1. No Portal do Azure da nuvem privada, faça o download do arquivo de configurações de publicação ou contate o administrador para obter um arquivo de configurações de publicação. (O arquivo tem a extensão `.publishsettings`.)

1. No **Gerenciador de Servidores** do Visual Studio, clique com o botão direito do mouse no nó **Azure** e selecione **Gerenciar e Filtrar Assinaturas**.

    ![Comando Gerenciar assinaturas](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Na caixa de diálogo **Gerenciar Assinaturas do Microsoft Azure**, selecione a guia **Certificados** e, em seguida, **Importar**.

    ![Importação de certificados do Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Na caixa de diálogo **Importar Assinaturas do Microsoft Azure**, selecione **Procurar**.

    ![Botão Procurar na caixa de diálogo Importar Assinaturas do Microsoft Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Na caixa de diálogo **Abrir**, procure o diretório em que você salvou o arquivo de configurações de publicação, selecione o arquivo e, em seguida, selecione **Abrir**.

    ![Selecionar o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Ao retornar para a caixa de diálogo **Importar Assinaturas do Microsoft Azure**, selecione **Importar**.

    ![Importar o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Os certificados são importados do arquivo de configurações de publicação para o Visual Studio, e agora é possível interagir com os recursos de nuvem privada.
