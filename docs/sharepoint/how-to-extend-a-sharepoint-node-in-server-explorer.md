---
title: 'Como: estender um nó do SharePoint no Gerenciador de Servidores | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ea556d18641b96ea6a38ef5abf6efe4c93a44cdf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015018"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>Como: estender um nó do SharePoint no Gerenciador de Servidores
  Você pode estender nós sob o nó **conexões do SharePoint** no **Gerenciador de servidores**. Isso é útil quando você deseja adicionar novos nós filho, itens de menu de atalho ou propriedades a um nó existente. Para obter mais informações, consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>Para estender um nó do SharePoint no Gerenciador de Servidores

1. Crie um projeto de biblioteca de classes.

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint

    - Microsoft. VisualStudio. SharePoint. Explorer. Extensions

    - System. ComponentModel. composição

3. Crie uma nova classe que implemente a interface <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>.

4. Adicione o <xref:System.ComponentModel.Composition.ExportAttribute> atributo à classe. Esse atributo permite que o Visual Studio descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> tipo para o construtor de atributo.

5. Adicione o <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> atributo à classe. Esse atributo especifica o identificador de cadeia de caracteres para o tipo de nó que você deseja estender.

     Para especificar tipos de nó internos fornecidos pelo Visual Studio, passe um dos seguintes valores de enumeração para o construtor de atributo:

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: Use esses valores para especificar nós de conexão do site (os nós que exibem URLs do site), nós do site ou todos os outros nós pai no **Gerenciador de servidores**.

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: Use esses valores para especificar um dos nós internos que representam um componente individual em um site do SharePoint, como um nó que representa uma lista, um campo ou um tipo de conteúdo.

6. Em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> método, use membros do parâmetro *NodeType* para adicionar recursos ao nó. Esse parâmetro é um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> objeto que fornece acesso aos eventos definidos na <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> interface. Por exemplo, você pode manipular os seguintes eventos:

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>: Manipule esse evento para adicionar novos nós filho ao nó. Para obter mais informações, consulte [como: adicionar um nó personalizado do SharePoint ao Gerenciador de servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md).

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>: Manipule esse evento para adicionar um item de menu de atalho personalizado ao nó.

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>: Manipule esse evento para adicionar propriedades personalizadas ao nó. As propriedades aparecem na janela **Propriedades** quando o nó é selecionado.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como criar dois tipos diferentes de extensões de nó:

- Uma extensão que adiciona um item de menu de contexto aos nós do site do SharePoint. Quando você clica no item de menu, ele exibe o nome do nó que foi clicado.

- Uma extensão que adiciona uma propriedade personalizada chamada **ContosoExampleProperty** a cada nó que representa um campo chamado **Body**.

  [!code-csharp[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs#9)]
  [!code-vb[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb#9)]

  Essa extensão adiciona uma propriedade de cadeia de caracteres editável aos nós. Você também pode criar propriedades personalizadas que exibem dados somente leitura do servidor do SharePoint. Para obter um exemplo que demonstra como fazer isso, consulte [passo a passos: estender Gerenciador de servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- Microsoft. VisualStudio. SharePoint. Explorer. Extensions

- System. ComponentModel. composição

- System.Windows.Forms

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão de **Gerenciador de servidores** , crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Como: adicionar um nó personalizado do SharePoint a Gerenciador de Servidores](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
