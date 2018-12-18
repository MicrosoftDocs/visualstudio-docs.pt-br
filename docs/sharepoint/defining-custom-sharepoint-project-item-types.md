---
title: Definindo tipos de Item de projeto personalizado do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f32f429186aa0c4a657503ca9744bf570d624f25
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49869503"
---
# <a name="define-custom-sharepoint-project-item-types"></a>Definir tipos personalizados de item de projeto do SharePoint
  Defina um novo tipo de item de projeto do SharePoint quando você deseja criar um novo tipo de item de projeto do SharePoint. Por exemplo, o Visual Studio não inclui itens de projeto do SharePoint para adicionar campos ou ações personalizadas para um site do SharePoint. Você pode definir seus próprios tipos de itens de projeto do SharePoint para a criação de campos, ações personalizadas ou outros tipos de componentes do SharePoint.  
  
## <a name="tasks-for-defining-sharepoint-project-item-types"></a>Tarefas para definir tipos de item de projeto do SharePoint
 Para definir um tipo de item de projeto personalizado, crie um assembly de extensão do Visual Studio que implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface. Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).  
  
 Quando você define um tipo de item de projeto personalizado, você também pode adicionar a seguinte funcionalidade para o item de projeto:  
  
- Adicione um item de menu de atalho para o item de projeto. O item de menu é exibido quando você abre o menu de atalho para o item de projeto em **Gerenciador de soluções** clicando com o item de projeto ou selecioná-la e, em seguida, escolhendo o **Shift** +  **F10** chaves. Para obter mais informações, consulte [como: adicionar um item de menu de atalho para um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md).  
  
- Adicione uma propriedade personalizada para o item de projeto. A propriedade aparece na **propriedades** janela quando você escolhe o item de projeto no **Gerenciador de soluções**. Para obter mais informações, consulte [como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md).  
  
  Para habilitar outros desenvolvedores a usar o item de projeto no Visual Studio, crie um arquivo. spdata e criar um modelo de item ou o modelo de projeto que está associado com o item de projeto. Para obter mais informações, consulte [criar um item modelos e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>Entender a relação entre tipos de item de projeto e instâncias de item de projeto
 Quando você define um tipo de item de projeto do SharePoint, o Visual Studio carrega sua extensão quando um item de projeto do tipo associado é adicionado a um projeto do SharePoint. Por exemplo, se você definir uma nova **ação personalizada** tipo de item de projeto, o Visual Studio carrega sua extensão quando um usuário adiciona uma **ação personalizada** item de projeto a um projeto. Visual Studio usa a mesma instância de sua extensão para todas as instâncias do tipo de item de projeto associado. No exemplo anterior, se o usuário adiciona um segundo **ação personalizada** de item de projeto ao projeto, a mesma instância de sua extensão é usada para personalizar o segundo item de projeto.  
  
 Para acessar uma instância específica do seu tipo de item de projeto, lidar com um dos <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> eventos do *projectItemTypeDefinition* parâmetro em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método. Por exemplo, para determinar quando um item de projeto de seu tipo personalizado é adicionado a um projeto, manipular o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> eventos. Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)   
 [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)   
 [Como: adicionar um item de menu de atalho para um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)   
 [Criar modelos de projeto do SharePoint para itens de projeto e modelos de item](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Passo a passo: Criar o item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)   
 [Passo a passo: Criar item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)   
 [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)   
 [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)   
 [Implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)  
  
