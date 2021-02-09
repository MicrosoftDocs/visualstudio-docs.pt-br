---
title: 'Como: editar uma configuração de implantação do SharePoint | Microsoft Docs'
description: Saiba como criar uma configuração de implantação do SharePoint ou modificar uma configuração de implantação existente.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 59354537f0c1f22534395da1e0ed3db3929a14a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913653"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>Como: editar uma configuração de implantação do SharePoint
  Você pode criar uma configuração de implantação ou modificar uma configuração de implantação existente. Por exemplo, você pode executar uma única etapa ou alterar a ordem das etapas no processo de implantação. Talvez você queira criar ou modificar as configurações de implantação porque as configurações internas e adicionadas programaticamente não podem ser alteradas.

## <a name="create-a-sharepoint-deployment-configuration"></a>Criar uma configuração de implantação do SharePoint

#### <a name="to-create-a-sharepoint-deployment-configuration"></a>Para criar uma configuração de implantação do SharePoint

1. Em **Gerenciador de soluções**, escolha um projeto do SharePoint e, na barra de menus, escolha **projeto**,**Propriedades** do _ProjectName_.

2. Na guia **SharePoint** , escolha o botão **novo** .

     A caixa de diálogo **Adicionar nova configuração de implantação** é exibida.

3. Na caixa de texto **nome** , insira um nome para a configuração de implantação.

4. No painel **etapas de implantação disponíveis** , escolha as etapas que você deseja adicionar à configuração de implantação, escolha o botão ( **>** ) e, em seguida, escolha o botão **OK** .

    > [!NOTE]
    > Se você tiver configurado um comando de pré-implantação ou um comando pós-implantação, essas etapas só são executadas se você adicioná-las a uma configuração de implantação personalizada.

## <a name="change-the-active-deployment-configuration"></a>Alterar a configuração de implantação ativa

#### <a name="to-change-the-active-deployment-configuration"></a>Para alterar a configuração de implantação ativa

1. Em **Gerenciador de soluções**, escolha um projeto do SharePoint e, na barra de menus, escolha   >  **\<*ProjectName*> Propriedades** do projeto.

2. Escolha a guia **SharePoint** .

3. Na caixa de listagem **configuração de implantação ativa** , escolha o nome da configuração de implantação que você deseja usar.

## <a name="see-also"></a>Consulte também
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
