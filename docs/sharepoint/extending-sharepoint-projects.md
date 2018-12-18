---
title: Estendendo projetos do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 56e714f910a2421a909cba6714e65d21b66991ce
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49835833"
---
# <a name="extend-sharepoint-projects"></a>Estender projetos do SharePoint
  Crie uma extensão de projeto quando você deseja personalizar recursos de nível de projeto de projetos do SharePoint. Por exemplo, você pode adicionar propriedades de projeto personalizado ou responder a eventos de nível de projeto que são gerados quando o usuário desenvolve uma solução do SharePoint no Visual Studio.  
  
## <a name="create-project-extensions"></a>Criar extensões do projeto
 Para estender um item de projeto, crie um assembly de extensão do Visual Studio que implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface. Para obter mais informações, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).  
  
 Quando você cria uma extensão de projeto, você também pode adicionar a seguinte funcionalidade para os projetos do SharePoint:  
  
- Adicione um item de menu de atalho. O item de menu é exibido quando você abre o menu de atalho para um nó de projeto do SharePoint no **Gerenciador de soluções** clicando duas vezes no nó ou selecioná-la e, em seguida, escolhendo o **Shift** +  **F10** chaves. Para obter mais informações, consulte [como: adicionar um item de menu de atalho a projetos do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md).  
  
- Adicione uma propriedade personalizada. A propriedade aparece na **propriedades** janela quando você escolhe um projeto do SharePoint na **Gerenciador de soluções**. Para obter mais informações, consulte [como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md).  
  
  Para um passo a passo que demonstra como criar, implantar e testar uma extensão de projeto, consulte [instruções passo a passo: criar uma extensão de projeto do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md).  
  
## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>Entender a relação entre as extensões de projeto e instâncias do projeto
 Quando você cria uma extensão de projeto, a extensão carrega quando qualquer tipo de projeto do SharePoint é aberto no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] inclui vários modelos de projeto do SharePoint, como definições de listas, tipos de conteúdo e receptores de eventos. No entanto, há apenas um tipo de projeto do SharePoint. Os tipos de projeto que aparecem na **novo projeto** caixa de diálogo são apenas os modelos que agrupar um ou mais itens de projeto do SharePoint. Como há apenas um tipo de projeto do SharePoint, as extensões criadas para um projeto se aplicam a todos os projetos do SharePoint. Você não pode, por exemplo, criar uma extensão que se aplica somente a um **tipo de conteúdo** projeto.  
  
 Para acessar uma instância de projeto específico, lidar com um dos <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> eventos do *projectService* parâmetro em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método. Por exemplo, para determinar quando um projeto do SharePoint é adicionado a uma solução, manipular o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> eventos. Para obter mais informações, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)   
 [Como: adicionar um item de menu de atalho a projetos do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)   
 [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)   
 [Passo a passo: Criar uma extensão de projeto do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)   
 [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Estender os itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)   
 [Estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md)   
 [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)  
  
  
