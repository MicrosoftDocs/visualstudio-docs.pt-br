---
title: Preparar para publicar ou implantar um serviço de nuvem
description: Conheça os procedimentos para configurar serviços de conta de armazenamento e de nuvem e configurar seu aplicativo do Azure.
author: ghogen
manager: jillfra
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: 5cd458cca0a0b387ce816f2e7f5dde8153e08410
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280798"
---
# <a name="prepare-to-publish-or-deploy-a-cloud-service-from-visual-studio"></a>Preparar para publicar ou implantar um serviço de nuvem do Visual Studio

Para publicar um projeto de serviço de nuvem, você deve configurar os seguintes serviços, conforme descrito neste artigo:

* Um **serviço de nuvem** para executar suas funções no ambiente do Azure, e
* Uma **conta de armazenamento** que forneça acesso aos serviços de blob, fila e tabela.

## <a name="create-a-cloud-service"></a>Criar um Serviço de Nuvem

Um serviço de nuvem executa suas funções no ambiente do Azure. Você pode criar um serviço de nuvem no Visual Studio ou por meio do [Portal do Azure](https://portal.azure.com/), conforme descrito nas seções a seguir.

### <a name="create-a-cloud-service-from-visual-studio"></a>Criar um serviço de nuvem do Visual Studio

1. Com um projeto de Serviço de Nuvem criado anteriormente, clique com botão direito no projeto e selecione **Publicar**.
1. Se for necessário, entre com a conta da Microsoft ou da organização associada à sua assinatura do Azure e selecione **Avançar** para ir até a página **Configurações**.
1. Uma caixa de diálogo **Criar Serviço de Nuvem e a Conta de Armazenamento** aparece (se não aparecer, selecione **Criar Novo** na lista **Serviço de Nuvem**).
1. Insira um nome que não diferencia maiúsculas e minúsculas para seu serviço de nuvem, que forma parte de sua URL e deve ser exclusivo. Escolha também uma Região ou Grupo de Afinidade, e selecione uma opção de Replicação.

### <a name="create-a-cloud-service-through-the-azure-portal"></a>Criar um serviço de nuvem no portal do Azure

1. Entre no [portal do Azure](https://portal.azure.com/).
1. Selecione **Serviços de Nuvem (clássico)** no lado esquerdo da página.
1. Selecione **+ Adicionar**, depois forneça as informações necessárias (Nome DNS, assinatura, grupo de recursos e local). Não é necessário carregar um pacote no momento, você pode fazer isso mais tarde no Visual Studio.
1. Selecione **Criar** para concluir o processo.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Uma conta de armazenamento fornece acesso aos serviços de blob, fila e tabela. Você pode criar uma conta de armazenamento usando o Visual Studio ou o [Portal do Azure](https://portal.azure.com/).

### <a name="create-a-storage-account-from-visual-studio"></a>Criar uma conta de armazenamento no Visual Studio

1. No **Gerenciador de Soluções**, com um projeto de Serviço de Nuvem criado anteriormente, localize o nó **Serviços Conectados** dentro de um projeto de função, clique com o botão direito e selecione **Adicionar Serviço Conectado**. (No Visual Studio 2015, clique com o botão direito no nó **Armazenamento** e selecione **Criar Conta de Armazenamento**.)
1. Na lista **Serviços Conectados** exibida, selecione **Armazenamento de Nuvem com o Armazenamento do Azure**.
1. Na caixa de diálogo Armazenamento do Azure exibida, selecione **+ Criar Nova Conta de Armazenamento**, que mostra uma caixa de diálogo na qual você especifica sua assinatura, um nome para a conta, um tipo de preço, grupo de recursos e local.
1. Selecione **Criar** quando terminar. A nova conta de armazenamento aparece na lista de contas de armazenamento disponíveis em sua assinatura.
1. Selecione a conta e selecione **Adicionar**.

### <a name="create-a-storage-account-through-the-azure-portal"></a>Criar uma conta de armazenamento no Portal do Azure

1. Entre no [portal do Azure](https://portal.azure.com/).
1. Selecione **+ Novo** no painel à esquerda.
1. Selecione **Armazenamento** em "Azure Marketplace", depois **Conta de Armazenamento - blob, arquivo, tabela, fila** do lado direito.
1. Forneça as informações necessárias (nome, modelo de implantação e assim por diante.
1. Selecione **Criar** para concluir o processo.

## <a name="configure-your-app-to-use-the-storage-account"></a>Configurar seu aplicativo para usar a conta de armazenamento

Depois de criar uma conta de armazenamento, a conexão pelo Visual Studio atualiza automaticamente as configurações de serviço do projeto, incluindo URLs e teclas de acesso.

Se você criou um serviço de nuvem no Visual Studio usando **Adicionar Serviço Conectado**, você poderá verificar as conexões abrindo `ServiceConfiguration.Cloud.cscfg` e `ServiceConfiguration.Local.cscfg`.

Se você criou um serviço de nuvem por meio do Portal do Azure, execute as mesmas etapas em [Criar uma conta de armazenamento no Visual Studio](#create-a-storage-account-from-visual-studio), mas selecione a conta existente em vez de criar uma nova. Depois, o Visual Studio atualiza a configuração para você.

Para definir manualmente as configurações, use as páginas de propriedades no Visual Studio para a função aplicável em seu projeto de serviço de nuvem (clique com o botão direito na função e selecione **Propriedades**). Para saber mais, confira [Configurar uma cadeia de conexão para uma conta de armazenamento](vs-azure-tools-multiple-services-project-configurations.md#configuring-a-connection-string-for-a-storage-account).

### <a name="about-access-keys"></a>Sobre chaves de acesso

O Portal do Azure mostra as URLs que você pode usar para acessar recursos em cada um dos serviços de armazenamento do Azure e as chaves de acesso primária e secundária para sua conta. Você pode usar essas chaves para autenticar solicitações feitas nos serviços de armazenamento.

A chave de acesso secundária fornece o mesmo acesso à sua conta de armazenamento que a chave de acesso primária e é gerada como um backup, caso sua chave de acesso primária seja comprometida. Além disso, é recomendável que você gere novamente e regularmente suas chaves de acesso. Você pode modificar uma configuração de cadeia de conexão para usar a chave secundária enquanto gera novamente a chave primária, e então poderá modificá-la para usar a chave primária gerada enquanto gera novamente a chave secundária.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre publicação de aplicativos para o Azure do Visual Studio, consulte [Publicando um serviço de nuvem usando as ferramentas do Azure](vs-azure-tools-publishing-a-cloud-service.md).
