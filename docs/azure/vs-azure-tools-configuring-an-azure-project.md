---
title: Configurar um projeto de serviço de nuvem do Azure
description: Saiba como configurar um projeto de serviço de nuvem do Azure no Visual Studio, dependendo dos requisitos para o projeto.
author: ghogen
manager: jillfra
assetId: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/06/2017
ms.author: ghogen
ms.openlocfilehash: 1776aebbe827295cbc7902f72417bc57e03a4196
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280629"
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configurar um projeto de serviço de nuvem do Azure com o Visual Studio
Você pode configurar um projeto de serviço de nuvem do Azure, dependendo dos requisitos para o projeto. Você pode definir propriedades do projeto para as seguintes categorias:

- **Publicar um serviço de nuvem no Azure**: você pode definir uma propriedade para ter certeza de que um serviço de nuvem existente implantado no Azure não seja excluído acidentalmente.
- **Executar ou depurar um serviço de nuvem no computador local**: você pode selecionar uma configuração de serviço para usar e indicar se deseja iniciar o emulador de armazenamento do Azure.
- **Validar um pacote de serviço de nuvem quando ele é criado**: você pode optar por tratar todos os avisos como erros para que seja possível garantir que o pacote de serviço de nuvem seja implantado sem problemas.

## <a name="steps-to-configure-an-azure-cloud-service-project"></a>Etapas para configurar um projeto de serviço de nuvem do Azure
1. Abra ou crie um projeto de serviço de nuvem do Azure no Visual Studio

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, no menu de contexto, selecione **Propriedades**.

1. Na página de propriedades do projeto, selecione a guia **Desenvolvimento**.

    ![Menu Propriedades do projeto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Defina **Avisar antes de excluir uma implantação existente** como **Verdadeiro**. Essa configuração ajuda a garantir que você não exclua acidentalmente uma implantação existente no Azure

1. Selecione a **Configuração de serviço** desejada para indicar qual configuração de serviço deseja usar quando executar ou depurar o serviço de nuvem localmente. Para saber mais sobre como modificar uma configuração de serviço para uma função, confira [Configurar funções de serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Defina **Iniciar emulador de armazenamento do Azure** como **Verdadeiro** para iniciar o emulador de armazenamento do Azure ao executar ou depurar o serviço de nuvem localmente.

1. Defina **Tratar avisos como erros** como **Verdadeiro** para garantir que não seja possível publicar se houver erros de validação de pacote.

1. Defina **Usar portas de projeto Web** como **Verdadeiro** para garantir que sua função web use a mesma porta toda vez que ela iniciar localmente no IIS Express.

1. Na barra de ferramentas do Visual Studio, selecione **Salvar**.

## <a name="next-steps"></a>Próximas etapas
- [Configurando um projeto do Azure usando várias configurações de serviço](vs-azure-tools-multiple-services-project-configurations.md)
