---
title: Estendendo o nó conexões do SharePoint no Gerenciador de Servidores | Microsoft Docs
titleSuffix: ''
description: Estenda o nó conexões do SharePoint na janela Gerenciador de Servidores no Visual Studio. Adicione Propriedades personalizadas a nós. Obter dados para nós internos.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1f77e0044b8ae3c7456a31bb9c9153ba9e9f4c99
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218029"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>Estenda o nó conexões do SharePoint no Gerenciador de Servidores
  No Visual Studio, você pode se conectar a sites locais do SharePoint no computador de desenvolvimento usando o nó **conexões do SharePoint** na janela **Gerenciador de servidores** . Esse nó exibe muitos dos componentes de sites locais do SharePoint em um modo de exibição de árvore hierárquica. Por exemplo, você pode exibir as listas, as bibliotecas de documentos e os tipos de conteúdo em sites locais. Para obter mais informações sobre como usar **Gerenciador de servidores** para se conectar a sites locais do SharePoint, consulte [procurar conexões do SharePoint usando Gerenciador de servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md).

 Você pode estender o nó **conexões do SharePoint** criando extensões para os nós existentes ou criando um tipo de nó personalizado e adicionando-o à hierarquia de nós.

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>Tarefas para estender o nó conexões do SharePoint
 Para estender um nó existente, crie uma extensão do Visual Studio que implemente a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Ao estender um nó, você pode adicionar funcionalidade ao nó, como seus próprios itens de menu de atalho ou propriedades personalizadas. Para obter mais informações, consulte [como: estender um nó do SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).

 Para criar um tipo de nó personalizado, crie uma extensão do Visual Studio que implementa a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Crie um nó personalizado se desejar exibir componentes de sites do SharePoint que não são exibidos no **Gerenciador de servidores** por padrão. Por exemplo, **Gerenciador de servidores** não exibe a Galeria de Web Parts de um site do SharePoint por padrão, mas você pode adicionar um nó personalizado que faz isso. Para obter mais informações, consulte [como: adicionar um nó personalizado do SharePoint a Gerenciador de servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md) e [passo a passos: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).

## <a name="add-custom-properties-to-nodes"></a>Adicionar propriedades personalizadas a nós
 Ao estender um nó ou criar um tipo de nó personalizado, você pode adicionar propriedades personalizadas ao nó. As propriedades aparecem na janela **Propriedades** quando o nó é selecionado.

 Há dois tipos de propriedades personalizadas que você pode adicionar a um nó:

- Propriedades que exibem um conjunto de dados somente leitura do site do SharePoint. Os dados descrevem o componente do SharePoint que o nó representa. Para obter instruções que demonstram como fazer isso, consulte [Walkthrough: Extend Gerenciador de servidores to display Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).

- Propriedades que exibem dados personalizados de leitura/gravação. Para obter um exemplo de código que demonstra como fazer isso, consulte [como: estender um nó do SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).

## <a name="get-data-for-built-in-nodes"></a>Obter dados para nós internos
 Todos os nós internos fornecidos pelo Visual Studio incluem alguns dados sobre o componente do SharePoint que eles representam. Por exemplo, um nó que representa uma lista no site do SharePoint fornece alguns dados sobre a lista, como o título e a URL da exibição padrão da lista.

 Para acessar esses dados, recupere um objeto de dados da <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto que representa o nó no qual você está interessado. O tipo do objeto de dados depende do tipo do nó.

 O exemplo de código a seguir demonstra como obter o objeto de dados para um nó de lista. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: obter dados para um nó interno do SharePoint no Gerenciador de servidores](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md).

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet11":::

 A tabela a seguir lista os tipos de objeto de dados para cada tipo de nó interno.

|Tipo de nó|Tipo de objeto de dados|
|---------------|----------------------|
|Nó do site do SharePoint|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|Tipo de conteúdo|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|Recurso|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|Campo|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|Lista|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|Modelo de lista|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|Exibição de lista (Microsoft. SharePoint. SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|Associação de fluxo de trabalho|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|Modelo de fluxo de trabalho|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade, consulte [associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).

## <a name="see-also"></a>Confira também
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [Como: estender um nó do SharePoint no Gerenciador de Servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [Como: adicionar um nó personalizado do SharePoint a Gerenciador de Servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [Como: obter dados para um nó interno do SharePoint no Gerenciador de Servidores](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [Procurar conexões do SharePoint usando Gerenciador de Servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [Estenda as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
