---
title: Associando dados personalizados a extensões de ferramentas do SharePoint | Microsoft Docs
description: Associe dados personalizados a extensões de ferramentas do SharePoint. Veja uma lista de objetos que podem conter dados personalizados. Adicionar e recuperar dados personalizados.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5665fc28bacb76c6887cb7dcb1820ec9dc0d2b3a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215312"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>Associar dados personalizados a extensões de ferramentas do SharePoint
  Você pode adicionar dados personalizados a determinados objetos em extensões de ferramentas do SharePoint. Isso é útil quando você tem dados em uma parte da extensão que deseja acessar posteriormente de outro código em sua extensão. Em vez de implementar uma maneira personalizada de armazenar e acessar dados, você pode associar os dados a um objeto em sua extensão e, em seguida, recuperar os dados do mesmo objeto mais tarde.

 Adicionar dados personalizados a objetos também é útil quando você deseja preservar os dados que são relevantes para um item específico no Visual Studio. As extensões das ferramentas do SharePoint são carregadas apenas uma vez no Visual Studio, de modo que sua extensão pode funcionar com vários itens diferentes (como projetos, itens de projeto ou nós de **Gerenciador de servidores** ) a qualquer momento. Se você tiver dados personalizados que são relevantes apenas para um item específico, poderá adicionar os dados ao objeto que representa esse item.

 Quando você adiciona dados personalizados a objetos em extensões de ferramentas do SharePoint, os dados não persistem. Os dados estão disponíveis somente durante o ciclo de vida do objeto. Depois que o objeto é recuperado pela coleta de lixo, os dados são perdidos.

 Em extensões do sistema de projeto do SharePoint, você também pode salvar dados de cadeia de caracteres que persistem depois que uma extensão é descarregada. Para obter mais informações, consulte [salvando dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

## <a name="objects-that-can-contain-custom-data"></a>Objetos que podem conter dados personalizados
 Você pode adicionar dados personalizados a qualquer objeto no modelo de objeto de ferramentas do SharePoint que implementa a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> interface. Essa interface define apenas uma propriedade, <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> , que é uma coleção de objetos de dados personalizados. Os seguintes tipos implementam <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> :

- <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>

- <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>

- <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>

## <a name="add-and-retrieve-custom-data"></a>Adicionar e recuperar dados personalizados
 Para adicionar dados personalizados a um objeto em uma extensão de ferramentas do SharePoint, obtenha a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do objeto ao qual você deseja adicionar os dados e, em seguida, use o <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> método para adicionar os dados ao objeto.

 Para recuperar dados personalizados de um objeto em uma extensão de ferramentas do SharePoint, obtenha a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do objeto e, em seguida, use um dos seguintes métodos:

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. Esse método retornará **true** se o objeto de dados existir ou **false** se não existir. Você pode usar esse método para recuperar instâncias de tipos de valor ou tipos de referência.

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. Esse método retornará o objeto de dados se ele for encerrado, ou **NULL** se não existir. Você pode usar esse método somente para recuperar instâncias de tipos de referência.

  O exemplo de código a seguir determina se um determinado objeto de dados já está associado a um item de projeto. Se o objeto de dados ainda não estiver associado ao item do projeto, o código adicionará o objeto à <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do item do projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md).

  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet13":::
  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet13":::

## <a name="see-also"></a>Confira também
- [Conceitos e recursos de programação para extensões de ferramentas do SharePoint](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [Walkthrough: Criando um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [Walkthrough: estendendo Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
