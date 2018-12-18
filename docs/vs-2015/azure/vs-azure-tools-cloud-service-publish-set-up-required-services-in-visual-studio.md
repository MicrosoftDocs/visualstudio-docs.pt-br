---
title: Preparar para publicar ou implantar um serviço de nuvem do Visual Studio | Microsoft Docs
description: Conheça os procedimentos para configurar serviços de nuvem e armazenamento de conta e configurar seu aplicativo do Azure.
author: ghogen
manager: douge
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: d7643d87f60b953b9c0928571036c7890e4d11f0
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001320"
---
# <a name="prepare-to-publish-or-deploy-a-cloud-service-from-visual-studio"></a>Preparar para publicar ou implantar um serviço de nuvem usando o Visual Studio

Para publicar um projeto de serviço de nuvem, você deve configurar os serviços a seguir conforme descrito neste artigo:

* Um **serviço de nuvem** para executar suas funções no ambiente do Azure, e 
* Um **conta de armazenamento** que fornece acesso aos serviços Blob, fila e tabela.

## <a name="create-a-cloud-service"></a>Criar um serviço de nuvem

Um serviço de nuvem executa suas funções no ambiente do Azure. Você pode criar um serviço de nuvem no Visual Studio ou por meio de [portal do Azure](https://portal.azure.com/) conforme descrito nas seções a seguir.

### <a name="create-a-cloud-service-from-visual-studio"></a>Criar um serviço de nuvem do Visual Studio

1. Com um projeto de serviço de nuvem criado anteriormente, clique com botão direito no projeto e selecione **publicar**.
1. Se necessário, entre com a Microsoft ou conta organizacional associada à sua assinatura do Azure e, em seguida, selecione **próxima** para ir para o **configurações** página.
1. Um **criar serviço de nuvem e conta de armazenamento** caixa de diálogo aparece (se não, selecione **criar nova** do **serviço de nuvem** lista).
1. Insira um nome diferencia maiusculas de minúsculas para seu serviço de nuvem, que faz parte da sua URL e deve ser exclusivo. Também escolha uma região ou grupo de afinidade e selecione uma opção de replicação.

### <a name="create-a-cloud-service-through-the-azure-portal"></a>Criar um serviço de nuvem por meio do portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com/).
1. Selecione **serviços de nuvem (clássico)** no lado esquerdo da página.
1. Selecione **+ adicionar**, em seguida, forneça as informações necessárias (nome DNS, assinatura, grupo de recursos e local). Não é necessário carregar um pacote no momento porque fazer isso mais tarde no Visual Studio.
1. Selecione **criar** para concluir o processo.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Uma conta de armazenamento fornece acesso aos serviços Blob, fila e tabela. Você pode criar uma conta de armazenamento por meio do Visual Studio ou o [portal do Azure](https://portal.azure.com/).

### <a name="create-a-storage-account-from-visual-studio"></a>Criar uma conta de armazenamento no Visual Studio

1. Na **Gerenciador de soluções** com um projeto de serviço de nuvem criado anteriormente, localize a **serviços conectados** nó dentro de um projeto de função, clique com botão direito e selecione **adicionar a serviço conectado**. (No Visual Studio 2015, clique com botão direito do **armazenamento** nó e selecione **criar conta de armazenamento**.)
1. No **serviços conectados** lista que aparece, selecione **armazenamento de nuvem com o armazenamento do Azure**.
1. Na caixa de diálogo armazenamento do Azure que aparece, selecione **+ criar nova conta de armazenamento**, que abre uma caixa de diálogo na qual você especifica sua assinatura, um nome para a conta, um preço camada, grupo de recursos e local.
1. Selecione **criar** quando você terminar. A nova conta de armazenamento aparece na lista de contas de armazenamento disponíveis na sua assinatura.
1. Selecione a conta e selecione **adicionar**.

### <a name="create-a-storage-account-through-the-azure-portal"></a>Criar uma conta de armazenamento por meio do portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com/).
1. Selecione **+ novo** no canto superior esquerdo.
1. Selecione **armazenamento** em "Azure Marketplace,", em seguida, **conta de armazenamento - blob, arquivo, tabela, fila** do lado direito.
1. Forneça as informações necessárias (nome, modelo de implantação e assim por diante.
1. Selecione **criar** para concluir o processo.

## <a name="configure-your-app-to-use-the-storage-account"></a>Configurar seu aplicativo para usar a conta de armazenamento

Depois de criar uma conta de armazenamento, conectando a ele do Visual Studio automaticamente atualiza as configurações de serviço para o projeto, incluindo URLs e chaves de acesso.

Se você criou um serviço de nuvem do Visual Studio usando o **Adicionar serviço conectado**, você pode verificar as conexões abrindo `ServiceConfiguration.Cloud.cscfg` e `ServiceConfiguration.Local.cscfg`.

Se você criou um serviço de nuvem por meio do portal do Azure, siga as mesmas etapas em [criar uma conta de armazenamento do Visual Studio](#create-a-storage-account-from-visual-studio) , mas selecione a conta existente em vez de criar um novo. Visual Studio, em seguida, atualiza a configuração para você.

Para configurar as configurações manualmente, usam as páginas de propriedades no Visual Studio para a função aplicável em seu projeto de serviço de nuvem (função com o botão direito e selecione **propriedades**). Para obter mais informações, consulte [Configurando uma cadeia de conexão para uma conta de armazenamento](vs-azure-tools-multiple-services-project-configurations.md#configuring-a-connection-string-for-a-storage-account).

### <a name="about-access-keys"></a>Sobre chaves de acesso

O portal do Azure mostra as URLs que você pode usar para acessar recursos em cada um dos serviços de armazenamento do Azure e as chaves de acesso primária e secundária para sua conta. Você pode usar essas chaves para autenticar solicitações feitas nos serviços de armazenamento.

A chave de acesso secundária fornece o mesmo acesso à sua conta de armazenamento como a chave de acesso primária e é gerada como um backup de sua chave de acesso primário for comprometido. Além disso, é recomendável que você regenere as chaves de acesso com regularidade. Você pode modificar uma configuração de cadeia de caracteres de conexão para usar a chave secundária enquanto você regenera a chave primária, em seguida, você pode modificá-lo para usar a chave primária gerada enquanto você regenera a chave secundária.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a publicação de aplicativos para o Azure do Visual Studio, consulte [publicando um serviço de nuvem usando as ferramentas do Azure](vs-azure-tools-publishing-a-cloud-service.md).
