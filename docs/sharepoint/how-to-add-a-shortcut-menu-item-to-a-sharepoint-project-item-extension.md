---
title: 'Como: adicionar um Item de Menu de atalho para uma extensão de Item de projeto do SharePoint | Microsoft Docs'
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
ms.openlocfilehash: 1a3e92d3131fb52342eb2d5ee10abd13a9dd005e
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36756039"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>Como: adicionar um item de menu de atalho para uma extensão de item de projeto do SharePoint
  Você pode adicionar um item de menu de atalho a um item de projeto do SharePoint existente, usando uma extensão de item de projeto. O item de menu é exibido quando um usuário clica o item de projeto no **Gerenciador de soluções**.  
  
 As etapas a seguir pressupõem que você já tenha criado uma extensão de item de projeto. Para obter mais informações, consulte [como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).  
  
### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>Para adicionar um item de menu de atalho em uma extensão de item de projeto  
  
1.  No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método de seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação, o identificador a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento do *projectItemType* parâmetro.  
  
2.  No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> evento, adicione um novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> do objeto para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> ou <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> coleção do parâmetro de argumentos de evento.  
  
3.  No <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> manipulador de eventos para o novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> do objeto, execute as tarefas que você deseja executar quando um usuário clica em seu item de menu de atalho.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como adicionar um item de menu de atalho para o item de projeto do receptor de eventos. Quando o usuário clica o item de projeto no **Gerenciador de soluções** e clica o **mensagem de gravação para a janela de saída** item de menu, o Visual Studio exibe uma mensagem no **saída**janela.  
  
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs#1)]  
  
 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem para o **saída** janela. Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer um projeto de biblioteca de classes com as referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)   
 [Como: adicionar uma propriedade a uma extensão de item de projeto do SharePoint](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)   
 [Estender os itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)   
 [Passo a passo: Estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)  
  
