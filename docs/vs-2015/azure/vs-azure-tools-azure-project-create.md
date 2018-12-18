---
title: Criando um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs
description: Saiba como criar um projeto de serviço de nuvem do Azure com o Visual Studio
author: ghogen
manager: douge
assetId: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 8149f60440becb3c7a8d0dc08b2a1a9c00fb171a
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001330"
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Criando um projeto de serviço de nuvem do Azure com o Visual Studio
As ferramentas do Azure para Visual Studio fornece um modelo de projeto que permite que você crie uma [serviço de nuvem do Azure](/azure/cloud-services/cloud-services-choose-me), que é um serviço simple de uso geral do Azure. Quando o projeto tiver sido criado, o Visual Studio permite que você configurar, depurar e implantar o serviço de nuvem no Azure.

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>Etapas para criar um projeto de serviço de nuvem do Azure no Visual Studio
Esta seção orienta você pela criação de um projeto de serviço de nuvem do Azure no Visual Studio com uma ou mais funções web.  

1. Inicie o Visual Studio como administrador.

1. No menu principal, selecione **arquivo** > **New** > **projeto**.

1. Selecione **Cloud** do Visual C# ou o Visual Basic em nós do modelo de projeto e selecione **serviço de nuvem do Azure** na lista de modelos.

    ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Especifique qual versão do .NET Framework que você deseja usar para desenvolver o projeto.

1. Insira um nome e local para seu projeto e um nome para a solução. 

1. Selecione **OK**.

1. No **novo serviço de nuvem do Microsoft Azure** caixa de diálogo, selecione as funções que você deseja adicionar e escolha o botão de seta para a direita para adicioná-los à sua solução.

    ![Selecionar novas funções de serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. Para renomear uma função que você adicionou, passe o mouse sobre a função na **novo serviço de nuvem do Microsoft Azure** caixa de diálogo e, no menu de contexto, selecione **Renomear**. Você também pode renomear uma função em sua solução (na **Gerenciador de soluções**) após ele ter sido adicionado.

    ![Renomeie a função do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

O projeto do Azure no Visual Studio tem associações aos projetos de função na solução. O projeto também inclui o *arquivo de definição de serviço* e *arquivo de configuração de serviço*:

- **Arquivo de definição de serviço** -define as configurações de tempo de execução de seu aplicativo, incluindo as funções que são necessárias, pontos de extremidade e tamanho da máquina virtual. 
- **Arquivo de configuração de serviço** – configura quantas instâncias de uma função são executadas e os valores das configurações definidas para uma função. 

Para obter mais informações sobre esses arquivos, consulte [Configure as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Próximas etapas
- [Gerenciando funções nos projetos de serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
