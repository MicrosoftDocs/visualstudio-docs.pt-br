---
title: Adicionar item de menu de atalho à extensão de item de projeto do SharePoint
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
ms.openlocfilehash: 5c0515fddc106418902cd2cca9fcba4c0e365da1
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014859"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>Como: adicionar um item de menu de atalho a uma extensão de item de projeto do SharePoint
  Você pode adicionar um item de menu de atalho a um item de projeto existente do SharePoint usando uma extensão de item de projeto. O item de menu é exibido quando um usuário clica com o botão direito do mouse no item do projeto no **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já criou uma extensão de item de projeto. Para obter mais informações, consulte [como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>Para adicionar um item de menu de atalho em uma extensão de item de projeto

1. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento do parâmetro *projectItemType* .

2. Em seu manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento, adicione um novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> coleção ou do parâmetro de argumentos de evento.

3. No <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> manipulador de eventos do novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto, execute as tarefas que você deseja executar quando um usuário clicar no item do menu de atalho.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar um item de menu de atalho ao item de projeto receptor de eventos. Quando o usuário clica com o botão direito do mouse no item de projeto no **Gerenciador de soluções** e clica no item de menu **gravar mensagem em janela de saída** , o Visual Studio exibe uma mensagem na janela **saída** .

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs#1)]

 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem na janela de **saída** . Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [Como: adicionar uma propriedade a uma extensão de item de projeto do SharePoint](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [Estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)
- [Walkthrough: estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
