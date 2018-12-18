---
title: Configurar um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs
description: Saiba como configurar um projeto de serviço de nuvem do Azure no Visual Studio, dependendo dos seus requisitos para o projeto.
author: ghogen
manager: douge
assetId: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/06/2017
ms.author: ghogen
ms.openlocfilehash: 7417bc117de7dc472f413dd9145944cad2d48bb4
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001315"
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configurar um projeto de serviço de nuvem do Azure com o Visual Studio
Você pode configurar um projeto de serviço de nuvem do Azure, dependendo dos seus requisitos para o projeto. Você pode definir propriedades do projeto para as seguintes categorias:

- **Publicar um serviço de nuvem no Azure** -você pode definir uma propriedade para certificar-se de que um serviço de nuvem existente implantado no Azure não seja excluído acidentalmente.
- **Executar ou depurar um serviço de nuvem no computador local** -você pode selecionar uma configuração de serviço para usar e indicar se deseja iniciar o emulador de armazenamento do Azure.
- **Validar um pacote de serviço de nuvem quando ele é criado** -você pode optar por tratar todos os avisos como erros, para que você possa garantir que o pacote de serviço de nuvem seja implantado sem problemas. 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a>Etapas para configurar um projeto de serviço de nuvem do Azure
1. Abra ou crie um projeto de serviço de nuvem no Visual Studio

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, no menu de contexto, selecione **propriedades**.
   
1. Na página de propriedades do projeto, selecione a **desenvolvimento** guia.

    ![Menu de propriedades do projeto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Definir **Avisar antes de excluir uma implantação existente** à **verdadeiro**. Essa configuração ajuda a garantir que você não exclua acidentalmente uma implantação existente no Azure

1. Selecione o desejado **configuração do serviço** para indicar qual configuração de serviço para o qual você deseja usar quando você executa ou depura seu serviço de nuvem localmente. Para obter mais informações sobre como modificar uma configuração de serviço para uma função, consulte [como configurar as funções para um serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Definir **emulador de armazenamento do Azure inicie** à **verdadeiro** para iniciar o emulador de armazenamento do Azure quando você executa ou depura seu serviço de nuvem localmente.

1. Definir **tratar avisos como erros** à **verdadeiro** para garantir que você não pode publicar se houver erros de validação de pacote.

1. Definir **usar portas de projeto da web** à **verdadeiro** para certificar-se de que sua função web usa a mesma porta de cada vez que ela iniciar localmente no IIS Express.

1. Na barra de ferramentas do Visual Studio, selecione **salvar**.

## <a name="next-steps"></a>Próximas etapas
- [Configurar um projeto do Azure usando várias configurações de serviço](vs-azure-tools-multiple-services-project-configurations.md)

