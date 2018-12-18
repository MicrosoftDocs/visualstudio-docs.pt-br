---
title: 'Como: criar uma extensão de Item de projeto do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 93459096e6d88ce3754c32bf7f61a3cf369cbeba
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118462"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>Como: criar uma extensão de item de projeto do SharePoint
  Crie uma extensão de item de projeto quando você deseja adicionar funcionalidade a um item de projeto do SharePoint que já está instalado no Visual Studio. Para obter mais informações, consulte [itens de projeto do SharePoint estender](../sharepoint/extending-sharepoint-project-items.md).  
  
### <a name="to-create-a-project-item-extension"></a>Para criar uma extensão de item de projeto  
  
1.  Crie um projeto de biblioteca de classes.  
  
2.  Adicione referências aos assemblies a seguir:  
  
    -   Microsoft.VisualStudio.SharePoint  
  
    -   System.ComponentModel.Composition  
  
3.  Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>.  
  
4.  Adicione os seguintes atributos à classe:  
  
    -   <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descobrir e carregar seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação. Passar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> tipo para o construtor de atributo.  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Em uma extensão de item de projeto, este atributo identifica o item de projeto que você deseja estender. Passe a ID do item de projeto para o construtor de atributo. Para obter uma lista de IDs de itens de projeto que estão incluídos com o Visual Studio, consulte [itens de projeto do SharePoint estender](../sharepoint/extending-sharepoint-project-items.md).  
  
5.  Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método, use os membros a *projectItemType* parâmetro para definir o comportamento da sua extensão. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto que fornece acesso para os eventos definidos na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> interfaces. Para acessar uma instância específica do tipo de item de projeto que você está estendendo, manipular <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> eventos, como <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized>.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como criar uma extensão simples para o item de projeto do receptor de eventos. Cada vez que o usuário adiciona um item de projeto do receptor de eventos para um projeto do SharePoint, essa extensão grava uma mensagem para o **saída** janela e **lista de erros** janela.  
  
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs#1)]
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb#1)]  
  
 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem para o **saída** janela e **lista de erros** janela. Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Estender os itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)   
 [Passo a passo: Estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)  
  
  
