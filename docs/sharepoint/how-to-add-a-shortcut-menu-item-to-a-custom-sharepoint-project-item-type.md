---
title: Adicionar item de menu de atalho ao tipo de item de projeto personalizado do SharePoint
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eef99509048b1dd54576a20449b9d4f51c11439e
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014875"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>Como: adicionar um item de menu de atalho a um tipo personalizado de item de projeto do SharePoint
  Ao definir um tipo de item de projeto personalizado do SharePoint, você pode adicionar um item de menu de atalho ao item de projeto. O item de menu é exibido quando um usuário clica com o botão direito do mouse no item do projeto no **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já definiu seu próprio tipo de item de projeto do SharePoint. Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>Para adicionar um item de menu de atalho a um tipo de item de projeto personalizado

1. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento do parâmetro *projectItemTypeDefinition* .

2. Em seu manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento, adicione um novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> coleção ou do parâmetro de argumentos de evento.

3. No <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> manipulador de eventos para o novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto, execute as tarefas que você deseja executar quando um usuário escolhe o item de menu de atalho.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar um item de menu de contexto a um tipo de item de projeto personalizado. Quando o usuário abre o menu de atalho do item de projeto no **Gerenciador de soluções** e escolhe a **mensagem de gravação para janela de saída** item de menu, o Visual Studio exibe uma mensagem na janela de **saída** .

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs#4)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb#4)]

 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem na janela de **saída** . Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-project-item"></a>Implantar o item de projeto
 Para permitir que outros desenvolvedores usem seu item de projeto, crie um modelo de projeto ou um modelo de item de projeto. Para obter mais informações, consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

 Para implantar o item de projeto, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly, o modelo e outros arquivos que você deseja distribuir com o item de projeto. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [Definindo tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
