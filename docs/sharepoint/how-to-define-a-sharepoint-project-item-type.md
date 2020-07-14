---
title: Como definir um tipo de item de projeto do SharePoint | Microsoft Docs
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
ms.openlocfilehash: ae709bf2d81e2b8b00dc984602c0426fdf272ebd
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016861"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>Como definir um tipo de item de projeto do SharePoint
  Defina um tipo de item de projeto quando desejar criar um item de projeto personalizado do SharePoint. Para obter mais informações, consulte [definindo tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md).

### <a name="to-define-a-project-item-type"></a>Para definir um tipo de item de projeto

1. Crie um projeto de biblioteca de classes.

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint

    - System. ComponentModel. composição

3. Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>.

4. Adicione os seguintes atributos à classe:

    - <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> tipo para o construtor de atributo.

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Em uma definição de tipo de item de projeto, esse atributo especifica o identificador de cadeia de caracteres para o novo item de projeto. Recomendamos que você use o formato *nome da empresa*. *nome do recurso* para ajudar a garantir que todos os itens do projeto tenham um nome exclusivo.

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. Esse atributo especifica o ícone a ser exibido para este item de projeto em **Gerenciador de soluções**. Esse atributo é opcional; Se você não aplicá-la à sua classe, o Visual Studio exibirá um ícone padrão para o item do projeto. Se você definir esse atributo, passe o nome totalmente qualificado de um ícone ou bitmap inserido no assembly.

5. Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método, use membros do parâmetro *projectItemTypeDefinition* para definir o comportamento do tipo de item do projeto. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto que fornece acesso aos eventos definidos nas <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> interfaces e. Para acessar uma instância específica do tipo de item do projeto, manipule <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> eventos como <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> .

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como definir um tipo de item de projeto simples. Esse tipo de item de projeto grava uma mensagem na janela de **saída** e **lista de erros** janela quando um usuário adiciona um item de projeto desse tipo a um projeto.

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb#2)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs#2)]

 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem na janela de **saída** e na janela de **lista de erros** . Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-project-item"></a>Implantar o item de projeto
 Para permitir que outros desenvolvedores usem seu item de projeto, crie um modelo de projeto ou um modelo de item de projeto. Para obter mais informações, consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

 Para implantar o item de projeto, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly, o modelo e outros arquivos que você deseja distribuir com o item de projeto. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Definir tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [Como: adicionar um item de menu de atalho a um tipo personalizado de item de projeto do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
