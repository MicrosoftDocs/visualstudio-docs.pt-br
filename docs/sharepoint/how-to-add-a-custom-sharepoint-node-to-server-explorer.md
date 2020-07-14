---
title: 'Como: adicionar um nó personalizado do SharePoint a Gerenciador de Servidores | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26a2ea6a7ccbfcc80275b55f9230f1a3152ab545
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017050"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>Como: adicionar um nó personalizado do SharePoint a Gerenciador de Servidores
  Você pode adicionar nós personalizados no nó **conexões do SharePoint** no **Gerenciador de servidores**. Isso é útil quando você deseja exibir componentes adicionais do SharePoint que não são exibidos no **Gerenciador de servidores** por padrão. Para obter mais informações, consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

 Para adicionar um nó personalizado, primeiro crie uma classe que defina o novo nó. Em seguida, crie uma extensão que adiciona o nó como um filho de um nó existente.

### <a name="to-define-the-new-node"></a>Para definir o novo nó

1. Crie um projeto de biblioteca de classes.

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint

    - Microsoft. VisualStudio. SharePoint. Explorer. Extensions

    - System. ComponentModel. composição

    - System.Drawing

3. Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>.

4. Adicione os seguintes atributos à classe:

    - <xref:System.ComponentModel.Composition.ExportAttribute>. Esse atributo permite que o Visual Studio descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> tipo para o construtor de atributo.

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. Em uma definição de nó, esse atributo especifica o identificador de cadeia de caracteres para o novo nó. Recomendamos que você use o formato *nome da empresa*. *nome do nó* para garantir que todos os nós tenham um identificador exclusivo.

5. Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> método, use membros do parâmetro *TypeDefinition* para configurar o comportamento do novo nó. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> objeto que fornece acesso aos eventos definidos na <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> interface.

     O exemplo de código a seguir demonstra como definir um novo nó. Este exemplo pressupõe que seu projeto contém um ícone chamado CustomChildNodeIcon como um recurso inserido.

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#6)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#6)]

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>Para adicionar o novo nó como um filho de um nó existente

1. No mesmo projeto que a definição de nó, crie uma classe que implemente a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface.

2. Adicione o <xref:System.ComponentModel.Composition.ExportAttribute> atributo à classe. Esse atributo permite que o Visual Studio descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> tipo para o construtor de atributo.

3. Adicione o <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> atributo à classe. Em uma extensão de nó, esse atributo especifica o identificador de cadeia de caracteres para o tipo de nó que você deseja estender.

     Para especificar tipos de nó internos fornecidos pelo Visual Studio, passe um dos seguintes valores de enumeração para o construtor de atributo:

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: Use esses valores para especificar nós de conexão do site (os nós que exibem URLs do site), nós do site ou todos os outros nós pai no **Gerenciador de servidores**.

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: Use esses valores para especificar um dos nós internos que representam um componente individual em um site do SharePoint, como um nó que representa uma lista, um campo ou um tipo de conteúdo.

4. Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> método, manipule o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> evento do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> parâmetro.

5. No <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> manipulador de eventos, adicione o novo nó à coleção de nós filho do <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> objeto que é exposto pelo parâmetro de argumentos de evento.

     O exemplo de código a seguir demonstra como adicionar o novo nó como um filho do nó do site do SharePoint no **Gerenciador de servidores**.

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#7)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#7)]

## <a name="complete-example"></a>Exemplo completo
 O exemplo de código a seguir fornece o código completo para definir um nó simples e adicioná-lo como um filho do nó do site do SharePoint no **Gerenciador de servidores**.

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#5)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#5)]

## <a name="compiling-the-code"></a>Compilando o código
 Este exemplo pressupõe que seu projeto contém um ícone chamado CustomChildNodeIcon como um recurso inserido. Este exemplo também requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

- System.Drawing

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão de **Gerenciador de servidores** , crie um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Como: estender um nó do SharePoint no Gerenciador de Servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
