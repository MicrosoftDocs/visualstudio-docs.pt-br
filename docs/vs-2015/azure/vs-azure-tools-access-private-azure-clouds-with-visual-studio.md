---
title: Acessando nuvens privadas do Azure com o Visual Studio | Microsoft Docs
description: Saiba como acessar recursos de nuvem privada usando o Visual Studio.
author: ghogen
manager: douge
assetId: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/13/2017
ms.author: ghogen
ms.openlocfilehash: 216b85e0ebf42b79c388ce217d548f2dce3c86b6
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001317"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Acessando nuvens privadas do Azure com o Visual Studio

Por padrão, o Visual Studio dá suporte a pontos de extremidade REST de nuvem do Azure. Neste artigo, você aprenderá como usar o certificado da sua nuvem privada para acessar e interagir com a nuvem privada no Visual Studio.

1. No portal do Azure para a nuvem privada, baixe o arquivo de configurações de publicação ou contate o administrador para um arquivo de configurações de publicação. (O arquivo tem a extensão `.publishsettings`.)

1. No Visual Studio **Gerenciador de servidores**, clique com botão direito do **Azure** nó e selecione **gerenciar e filtrar assinaturas**.

    ![Comando gerenciar assinaturas](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. No **gerenciar assinaturas do Microsoft Azure** caixa de diálogo, selecione o **certificados** guia e, em seguida, selecione **importação**.

    ![Importação de certificados do Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. No **importar assinaturas do Microsoft Azure** caixa de diálogo, selecione **procurar**.

    ![Botão Procurar na caixa de diálogo Importar assinaturas do Microsoft Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. No **aberto** caixa de diálogo, navegue até o diretório onde você salvou o arquivo de configurações de publicação, selecione o arquivo e, em seguida, selecione **abrir**.

    ![Selecione o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Quando retornado para o **importar assinaturas do Microsoft Azure** caixa de diálogo, selecione **importação**.

    ![Importe o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Os certificados são importados do arquivo de configurações de publicação para o Visual Studio, e você agora pode interagir com os recursos de nuvem privada.

