---
title: 'Como: definir um tipo de Item de projeto do SharePoint | Microsoft Docs'
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
ms.openlocfilehash: 3e35087481e1cdb536fddb4181f251e5595b365c
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118546"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>Como: definir um tipo de item de projeto do SharePoint
  Defina um tipo de item de projeto quando você deseja criar um item de projeto personalizado do SharePoint. Para obter mais informações, consulte [definindo tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md).  
  
### <a name="to-define-a-project-item-type"></a>Para definir um tipo de item de projeto  
  
1.  Crie um projeto de biblioteca de classes.  
  
2.  Adicione referências aos assemblies a seguir:  
  
    -   Microsoft.VisualStudio.SharePoint  
  
    -   System.ComponentModel.Composition  
  
3.  Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>.  
  
4.  Adicione os seguintes atributos à classe:  
  
    -   <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descobrir e carregar seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> implementação. Passar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> tipo para o construtor de atributo.  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Em uma definição de tipo de item de projeto, esse atributo especifica o identificador de cadeia de caracteres para o novo item de projeto. É recomendável que você use o formato *nome da empresa*. *nome do recurso* para certificar-se de que todos os itens de projeto tem um nome exclusivo.  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. Esse atributo especifica o ícone a ser exibido para este item de projeto no **Gerenciador de soluções**. Esse atributo é opcional. Se você não aplicá-lo à sua classe, o Visual Studio exibe um ícone padrão para o item de projeto. Se você definir esse atributo, passe o nome totalmente qualificado de um ícone ou bitmap que é inserido em seu assembly.  
  
5.  Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método, use os membros de *projectItemTypeDefinition* parâmetro para definir o comportamento do tipo de item de projeto. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto que fornece acesso para os eventos definidos na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> interfaces. Para acessar uma instância específica do seu tipo de item de projeto, manipular <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> eventos, como <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized>.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como definir um tipo de item de projeto simples. Esse tipo de item de projeto grava uma mensagem para o **saída** janela e **lista de erros** janela quando um usuário adiciona um item de projeto desse tipo para um projeto.  
  
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb#2)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs#2)]  
  
 Este exemplo usa o serviço de projeto do SharePoint para gravar a mensagem para o **saída** janela e **lista de erros** janela. Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-project-item"></a>Implantar o item de projeto  
 Para habilitar outros desenvolvedores a usar o item de projeto, crie um modelo de projeto ou um modelo de item de projeto. Para obter mais informações, consulte [criar um item modelos e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
 Para implantar o item de projeto, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensão (VSIX) do pacote para o assembly, o modelo e os outros arquivos que você deseja distribuir com o item de projeto. Para obter mais informações, consulte [das ferramentas de implantar extensões para o SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Criar modelos de projeto do SharePoint para itens de projeto e modelos de item](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)   
 [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)   
 [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)   
 [Como: adicionar um item de menu de atalho para um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)  
  
