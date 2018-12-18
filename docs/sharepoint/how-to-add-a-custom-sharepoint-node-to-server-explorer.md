---
title: 'Como: adicionar um nó personalizado do SharePoint no Gerenciador de servidores | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bb0ba7f09ae564a794792ad6f7a60f53f6f6422e
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36755635"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>Como: adicionar um nó do SharePoint personalizado ao Gerenciador de servidores
  Você pode adicionar nós personalizado sob o **conexões do SharePoint** nó no **Gerenciador de servidores**. Isso é útil quando você deseja exibir componentes adicionais do SharePoint que não são exibidos na **Gerenciador de servidores** por padrão. Para obter mais informações, consulte [estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).  
  
 Para adicionar um nó personalizado, primeiro crie uma classe que define o novo nó. Em seguida, crie uma extensão que adiciona o nó como um filho de um nó existente.  
  
### <a name="to-define-the-new-node"></a>Para definir o novo nó  
  
1.  Crie um projeto de biblioteca de classes.  
  
2.  Adicione referências aos assemblies a seguir:  
  
    -   Microsoft.VisualStudio.SharePoint  
  
    -   Microsoft.VisualStudio.SharePoint.Explorer.Extensions  
  
    -   System.ComponentModel.Composition  
  
    -   System.Drawing  
  
3.  Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>.  
  
4.  Adicione os seguintes atributos à classe:  
  
    -   <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descobrir e carregar seu <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> implementação. Passar o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> tipo para o construtor de atributo.  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. Em uma definição de nó, esse atributo especifica o identificador de cadeia de caracteres para o novo nó. É recomendável que você use o formato *nome da empresa*. *nome do nó* para certificar-se de que todos os nós têm um identificador exclusivo.  
  
5.  Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> método, use os membros de *typeDefinition* parâmetro para configurar o comportamento do novo nó. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> objeto que fornece acesso para os eventos definidos na <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> interface.  
  
     O exemplo de código a seguir demonstra como definir um novo nó. Este exemplo assume que seu projeto contém um ícone chamado CustomChildNodeIcon como um recurso inserido.  
  
     [!code-vb[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#6)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#6)]  
  
### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>Para adicionar o novo nó como um filho de um nó existente  
  
1.  No mesmo projeto que sua definição de nó, crie uma classe que implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface.  
  
2.  Adicionar o <xref:System.ComponentModel.Composition.ExportAttribute> à classe de atributo. Esse atributo permite que o Visual Studio descobrir e carregar seu <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> implementação. Passar o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> tipo para o construtor de atributo.  
  
3.  Adicionar o <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> à classe de atributo. Em uma extensão de nó, esse atributo especifica o identificador de cadeia de caracteres para o tipo de nó que você deseja estender.  
  
     Para especificar os tipos de nó internas fornecidos pelo Visual Studio, passe um dos seguintes valores de enumeração para o construtor de atributo:  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: Use esses valores para especificar nós de conexão de site (os nós que exibem as URLs de site), de nós, ou todos os outros nós pai no site **Gerenciador de servidores**.  
  
    -   <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: Use esses valores para especificar um de nós internos que representam um componente individual em um site do SharePoint, como um nó que representa uma lista, campo ou tipo de conteúdo.  
  
4.  Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> método, o identificador a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> evento do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> parâmetro.  
  
5.  No <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> manipulador de eventos, adicione o novo nó à coleção de nós filho do <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> objeto que é exposto pelo parâmetro de argumentos de evento.  
  
     O exemplo de código a seguir demonstra como adicionar o novo nó como um filho do nó no site do SharePoint **Gerenciador de servidores**.  
  
     [!code-vb[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#7)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#7)]  
  
## <a name="complete-example"></a>Exemplo completo
 O exemplo de código a seguir fornece o código completo para definir um nó simple e adicioná-lo como um filho do nó no site do SharePoint **Gerenciador de servidores**.  
  
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#5)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#5)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo assume que seu projeto contém um ícone chamado CustomChildNodeIcon como um recurso inserido. Este exemplo também requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
-   System.Drawing  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar o **Gerenciador de servidores** extensão, crie um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantem extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)   
 [Como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)   
 [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)  
  
  
