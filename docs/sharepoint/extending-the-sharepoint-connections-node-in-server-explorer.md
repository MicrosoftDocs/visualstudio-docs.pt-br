---
title: Estendendo o nó de conexões do SharePoint no Gerenciador de servidores | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f7211d31b8e57a88d3f6a5a585e912dd267cf943
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36325580"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>Estender o nó de conexões do SharePoint no Gerenciador de servidores
  No Visual Studio, você pode se conectar a sites locais do SharePoint no computador de desenvolvimento usando o **conexões do SharePoint** nó na **Server Explorer** janela. Esse nó exibe muitos dos componentes de sites locais do SharePoint em uma exibição de árvore hierárquica. Por exemplo, você pode exibir a listas, bibliotecas de documentos e tipos de conteúdo em sites locais. Para obter mais informações sobre como usar **Gerenciador de servidores** para se conectar a sites locais do SharePoint, consulte [procurar conexões do SharePoint usando o Gerenciador de servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md).  
  
 Você pode estender a **conexões do SharePoint** nó Criando extensões para nós existentes ou criando um tipo de nó personalizados e adicioná-lo para a hierarquia de nós.  
  
## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>Tarefas para estender o nó de conexões do SharePoint
 Para estender um nó existente, criar uma extensão do Visual Studio que implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Quando você estende um nó, você pode adicionar funcionalidade para o nó, como seus próprios itens de menu de atalho ou propriedades personalizadas. Para obter mais informações, consulte [como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).  
  
 Para criar um tipo de nó personalizados, crie uma extensão do Visual Studio que implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Criar um nó personalizado se você quiser exibir componentes de sites do SharePoint que não são exibidos na **Gerenciador de servidores** por padrão. Por exemplo, **Gerenciador de servidores** faz não exibir a Galeria de Web Part de um site do SharePoint por padrão, mas você pode adicionar um nó personalizado que faz isso. Para obter mais informações, consulte [como: adicionar um nó do SharePoint personalizado ao Gerenciador de servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md) e [passo a passo: estenda o Gerenciador de servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).  
  
## <a name="add-custom-properties-to-nodes"></a>Adicionar propriedades personalizadas para nós
 Ao estender um nó ou criar um tipo de nó personalizados, você pode adicionar propriedades personalizadas para o nó. As propriedades aparecem na **propriedades** janela quando o nó é selecionado.  
  
 Há dois tipos de propriedades personalizadas, que você pode adicionar a um nó:  
  
-   Propriedades que exibem um conjunto de dados somente leitura do site do SharePoint. Os dados descrevem o componente do SharePoint que o nó representa. Para um passo a passo que demonstra como fazer isso, consulte [instruções passo a passo: estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).  
  
-   Propriedades que exibem dados de leitura/gravação personalizado. Para obter um exemplo de código que demonstra como fazer isso, consulte [como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).  
  
## <a name="get-data-for-built-in-nodes"></a>Obter dados para nós internos
 Todos os nós internos fornecidos pelo Visual Studio incluem alguns dados sobre o componente do SharePoint que eles representam. Por exemplo, um nó que representa uma lista no site do SharePoint fornece alguns dados sobre a lista, como o título e a URL do modo de exibição padrão para a lista.  
  
 Para acessar esses dados, recuperar um objeto de dados das <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto que representa o nó que você está interessado. O tipo do objeto de dados depende do tipo de nó.  
  
 O exemplo de código a seguir demonstra como obter o objeto de dados para um nó de lista. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: obter dados para um nó SharePoint interno no Gerenciador de servidores](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md).  
  
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#11)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#11)]  
  
 A tabela a seguir lista os tipos de objeto de dados para cada tipo de nó interno.  
  
|Tipo de nó|Tipo de objeto de dados|  
|---------------|----------------------|  
|Nó do site do SharePoint|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|  
|Tipo de conteúdo|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|  
|Recurso|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|  
|Campo|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|  
|Lista|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|  
|Modelo de lista|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|  
|Modo de exibição de lista (SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|  
|Associação de fluxo de trabalho|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|  
|Modelo de fluxo de trabalho|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|  
  
 Para obter mais informações sobre como usar o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade, consulte [extensões de ferramentas associado a dados personalizados com o SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)   
 [Como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)   
 [Como: adicionar um nó do SharePoint personalizado ao Gerenciador de servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)   
 [Como: obter dados para um nó SharePoint interno no Gerenciador de servidores](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)   
 [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)   
 [Procurar conexões do SharePoint usando o Gerenciador de servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)   
 [Estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)  
  
  
