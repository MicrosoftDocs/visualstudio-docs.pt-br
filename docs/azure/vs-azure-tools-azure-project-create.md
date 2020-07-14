---
title: Criar um projeto de serviço de nuvem do Azure
description: Saiba como criar um projeto de serviço de nuvem do Azure com o Visual Studio
author: ghogen
manager: jillfra
assetId: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/19/2019
ms.author: ghogen
ms.openlocfilehash: ef5acada89d48ed91dbf5b0f5fe7c9801337d47f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280369"
---
# <a name="create-an-azure-cloud-service-project-with-visual-studio"></a>Criar um projeto de serviço de nuvem do Azure com o Visual Studio

O Visual Studio fornece um modelo de projeto que permite criar um [serviço de nuvem do Azure](/azure/cloud-services/cloud-services-choose-me), que é um serviço do Azure de uso geral simples. Após a criação do projeto, o Visual Studio permite configurar, depurar e implantar o serviço de nuvem no Azure.

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>Etapas para criar um projeto de serviço de nuvem do Azure no Visual Studio
Esta seção explica como criar um projeto de serviço de nuvem do Azure no Visual Studio com uma ou mais funções web.

::: moniker range="vs-2017"
1. Abra o Visual Studio como administrador.

1. No menu principal, selecione **Arquivo** > **Novo** > **Projeto**.

1. Selecione **Nuvem** nos nós do modelo de projeto do Visual C# ou Visual Basic e selecione **Serviço de Nuvem do Azure** na lista de modelos.

    ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Especifica qual versão do .NET Framework você deseja usar para desenvolver o projeto.

1. Insira um nome e local para seu projeto e um nome para a solução.

1. Selecione **OK**.
::: moniker-end
::: moniker range=">=vs-2019"
1. Na janela de início, escolha **Criar um novo projeto**.

1. Na caixa de pesquisa, digite *Nuvem* e, em seguida, escolha **Serviço de Nuvem do Azure**.

   ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/vs-2019/new-project-cloud-service.png)

1. Dê um nome ao projeto e escolha **Criar**.

   ![Dê um nome ao projeto](./media/vs-azure-tools-azure-project-create/vs-2019/new-project-cloud-service-2.png)
::: moniker-end

1. Na caixa de diálogo **Novo Serviço de Nuvem do Microsoft Azure**, selecione as funções que você deseja adicionar e escolha o botão de seta para a direita para adicioná-las à solução.

    ![Selecionar novas funções do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. Para renomear uma função adicionada, focalize a função na caixa de diálogo **Novo Serviço de Nuvem do Microsoft Azure** e, no menu de contexto, selecione **Renomear**. Você também pode renomear uma função na solução (no **Gerenciador de Soluções**) depois de adicioná-la.

    ![Renomear uma função do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

O projeto do Azure no Visual Studio tem associações aos projetos de função na solução. Ele também inclui o *arquivo de definição de serviço* e o *arquivo de configuração de serviço*:

- **Arquivo de definição de serviço** – define as configurações de tempo de execução para seu aplicativo, incluindo quais funções são necessárias, pontos de extremidade e tamanho da máquina virtual.
- **Arquivo de configuração de serviço** – configura quantas instâncias de uma função são executadas e os valores das configurações definidas para uma função.

Para obter mais informações sobre esses arquivos, consulte [Configurar as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Próximas etapas
- [Gerenciando funções em projetos de serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
