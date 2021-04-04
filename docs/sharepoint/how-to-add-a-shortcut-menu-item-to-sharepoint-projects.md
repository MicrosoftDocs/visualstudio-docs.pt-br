---
title: Como adicionar um item de menu de atalho a projetos do SharePoint | Microsoft Docs
titleSuffix: ''
description: Adicione um item de menu de atalho a um projeto do SharePoint no Visual Studio. O item de menu é exibido quando você clica com o botão direito do mouse em um nó de projeto no Gerenciador de Soluções.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 54ac53ad317f500e787baebfdfeb4a86dc917e06
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216807"
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

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb" id="Snippet1":::

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Confira também
- [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)
- [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
