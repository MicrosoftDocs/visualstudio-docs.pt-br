---
title: 'Como: editar uma configuração de implantação do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f06c26f2f274615058c46ecd45a6d73757b78db9
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43774788"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>Como: editar uma configuração de implantação do SharePoint
  Você pode criar uma configuração de implantação ou modificar uma configuração de implantação existente. Por exemplo, você pode executar uma única etapa ou alterar a ordem das etapas no processo de implantação. Você talvez queira criar ou modificar as configurações de implantação porque não não possível alterar as configurações internas e adicionadas programaticamente.  
  
## <a name="create-a-sharepoint-deployment-configuration"></a>Criar uma configuração de implantação do SharePoint  
  
#### <a name="to-create-a-sharepoint-deployment-configuration"></a>Para criar uma configuração de implantação do SharePoint  
  
1.  Na **Gerenciador de soluções**, escolha um projeto do SharePoint e, em seguida, na barra de menus, escolha **Project**, _ProjectName_**propriedades**.  
  
2.  Sobre o **SharePoint** guia, escolha o **New** botão.  
  
     O **adicionar nova configuração de implantação** caixa de diálogo é exibida.  
  
3.  No **nome** texto, digite um nome para a configuração de implantação.  
  
4.  No **as etapas de implantação disponíveis** painel, escolha as etapas que você deseja adicionar a configuração de implantação, escolha o (**>**) botão e, em seguida, escolha o **Okey** botão.  
  
    > [!NOTE]  
    >  Se você tiver configurado um comando de pré-implantação ou um comando de pós-implantação, essas etapas executadas somente se você adicioná-los a uma configuração de implantação personalizada.  
  
## <a name="change-the-active-deployment-configuration"></a>Alterar a configuração de implantação ativa  
  
#### <a name="to-change-the-active-deployment-configuration"></a>Para alterar a configuração de implantação ativa  
  
1.  Na **Gerenciador de soluções**, escolha um projeto do SharePoint e, em seguida, na barra de menus, escolha **Project** > **\<*ProjectName*> Propriedades**.  
  
2.  Escolha o **SharePoint** guia.  
  
3.  No **configuração de implantação ativa** caixa de listagem, escolha o nome da configuração de implantação que você deseja usar.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
