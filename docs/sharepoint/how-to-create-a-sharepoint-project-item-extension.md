---
title: 'Como: criar uma extensão de item de projeto do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 345bfa49da4bf5d5b73fe1d3f209675fe2814de2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015350"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>Como: criar uma extensão de item de projeto do SharePoint
  Crie uma extensão de item de projeto quando desejar adicionar funcionalidade a um item de projeto do SharePoint que já esteja instalado no Visual Studio. Para obter mais informações, consulte [estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md).

### <a name="to-create-a-project-item-extension"></a>Para criar uma extensão de item de projeto

1. Crie um projeto de biblioteca de classes.

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint

    - System. ComponentModel. composição

3. Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>.

4. Adicione os seguintes atributos à classe:

    - <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> tipo para o construtor de atributo.

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Em uma extensão de item de projeto, esse atributo identifica o item de projeto que você deseja estender. Passe a ID do item de projeto para o construtor de atributo. Para obter uma lista das IDs dos itens de projeto incluídos no Visual Studio, consulte [estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md).

5. Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método, use membros do parâmetro *projectItemType* para definir o comportamento de sua extensão. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto que fornece acesso aos eventos definidos nas <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> interfaces e. Para acessar uma instância específica do tipo de item de projeto que você está estendendo, manipule <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> eventos como <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> .

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como criar uma extensão simples para o item de projeto receptor de evento. Cada vez que o usuário adiciona um item de projeto receptor de eventos a um projeto do SharePoint, essa extensão grava uma mensagem na janela de **saída** e na janela de **lista de erros** .

 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs#1)]
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb#1)]

 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem na janela de **saída** e na janela de **lista de erros** . Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)
- [Walkthrough: estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
