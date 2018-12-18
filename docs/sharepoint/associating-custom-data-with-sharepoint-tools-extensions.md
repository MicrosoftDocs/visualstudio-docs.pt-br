---
title: Associando dados personalizados com o SharePoint extensões de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], associating custom data
- project items [SharePoint development in Visual Studio], associating custom data
- SharePoint project items, associating custom data
- SharePoint projects, associating custom data
- SharePoint development in Visual Studio, extensibility features
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 3e174440411e54d0f3960035874bd3b84b392c57
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939483"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>Associar dados personalizados a extensões de ferramentas do SharePoint
  Você pode adicionar dados personalizados a determinados objetos nas extensões de ferramentas do SharePoint. Isso é útil quando você tiver dados em uma parte de sua extensão que você deseja acessar mais tarde em outro código em sua extensão. Em vez de implementar de forma personalizada para armazenar e acessar dados, você pode associar os dados um objeto em sua extensão e, em seguida, recuperar os dados do mesmo objeto mais tarde.  
  
 Adicionando dados personalizados aos objetos também é útil quando você deseja preservar os dados que é relevantes para um item específico no Visual Studio. Extensões de ferramentas do SharePoint são carregados apenas uma vez no Visual Studio, portanto, sua extensão pode funcionar com vários itens diferentes (como projetos, itens, projeto ou **Gerenciador de servidores** nós) a qualquer momento. Se você tiver dados personalizados que são relevantes apenas para um item específico, você pode adicionar os dados para o objeto que representa o item.  
  
 Quando você adiciona dados personalizados para objetos em extensões de ferramentas do SharePoint, os dados não persistem. Os dados estão disponíveis somente durante o tempo de vida do objeto. Depois que o objeto seja recuperado pela coleta de lixo, os dados serão perdidos.  
  
 Nas extensões do sistema de projeto do SharePoint, você também pode salvar os dados de cadeia de caracteres que persiste depois que uma extensão é descarregada. Para obter mais informações, consulte [salvando dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).  
  
## <a name="objects-that-can-contain-custom-data"></a>Objetos que podem conter dados personalizados
 Você pode adicionar dados personalizados para qualquer objeto no modelo de objeto de ferramentas do SharePoint que implementa o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> interface. Essa interface define apenas uma propriedade, <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>, que é uma coleção de objetos personalizados. Os seguintes tipos de implementam <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject>:  
  
-   <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>  
  
-   <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>  
  
## <a name="add-and-retrieve-custom-data"></a>Adicionar e recuperar dados personalizados
 Para adicionar dados personalizados a um objeto em uma extensão de ferramentas do SharePoint, obtenha o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do objeto que você deseja adicionar os dados para e, em seguida, use o <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> método para adicionar os dados ao objeto.  
  
 Para recuperar dados personalizados de um objeto em uma extensão de ferramentas do SharePoint, obtenha o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do objeto e, em seguida, use um dos seguintes métodos:  
  
- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. Esse método retornará **verdadeira** se o objeto de dados existir, ou **falso** se ele não existir. Você pode usar esse método para recuperar instâncias de tipos de valor ou tipos de referência.  
  
- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. Esse método retorna os dados de objeto se ele for encerrada, ou **nulo** se ele não existir. Você pode usar esse método somente para recuperar instâncias de tipos de referência.  
  
  O exemplo de código a seguir determina se um determinado objeto de dados já está associado um item de projeto. Se o objeto de dados já não está associado com o item de projeto e, em seguida, o código adiciona o objeto a ser o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do item de projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md).  
  
  [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#13)]
  [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#13)]  
  
## <a name="see-also"></a>Consulte também
 [Conceitos de programação e recursos para extensões de ferramentas do SharePoint](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)   
 [Passo a passo: Criando um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)   
 [Passo a passo: Estendendo o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)   
 [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)   
 [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
   
 
