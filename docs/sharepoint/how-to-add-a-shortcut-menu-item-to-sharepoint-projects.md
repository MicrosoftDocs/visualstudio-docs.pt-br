---
title: Como adicionar um item de menu de atalho a projetos do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4e43d8d7717302eb8ab250935188bc2db3bdd66a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014845"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>Como: adicionar um item de menu de atalho a projetos do SharePoint
  Você pode adicionar um item de menu de atalho a qualquer projeto do SharePoint. O item de menu é exibido quando um usuário clica com o botão direito do mouse em um nó de projeto no **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já criou uma extensão de projeto. Para obter mais informações, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>Para adicionar um item de menu de atalho a projetos do SharePoint

1. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> evento do parâmetro *ProjectService* .

2. Em seu manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> evento, adicione um novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> coleção ou do parâmetro de argumentos de evento.

3. No <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> manipulador de eventos do novo <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> objeto, execute as tarefas que você deseja executar quando um usuário clicar no item do menu de atalho.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar um item de menu de atalho a nós de projeto do SharePoint no **Gerenciador de soluções**. Quando o usuário clica com o botão direito do mouse em um nó do projeto e clica no item de menu **gravar na janela de saída** , o Visual Studio exibe uma mensagem na janela **saída** . Este exemplo usa o serviço de projeto do SharePoint para exibir a mensagem. Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

 [!code-csharp[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs#1)]
 [!code-vb[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)
- [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
