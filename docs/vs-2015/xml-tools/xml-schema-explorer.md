---
title: XML Schema Explorer | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 32116de7bb88fe937980b02e1789830a27ca36b1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845869"
---
# <a name="xml-schema-explorer"></a>XML Schema Explorer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O XML Schema Explorer está integrado com o Microsoft Visual Studio e o Editor de XML para permitir que você trabalhe com esquemas da linguagem XSD. Quando você abre um arquivo de esquema XML, o **do conjunto de esquema** nó aparece no XML Schema Explorer. Todos os esquemas incluídos, importados ou redefinidos para o arquivo de destino, assim como os arquivos que são referenciados por meio de uma instrução `include` ou `import`, também aparecem no XML Schema Explorer.  
  
 O XML Schema Explorer permite que você faça o seguinte:  
  
- Obter uma visão geral rápido do conjunto de esquema.  
  
- Procurar e navegar na árvore.  
  
- Realizar pesquisas de palavra-chave e específicas do esquema. Para obter mais informações, consulte [procurando o conjunto de esquema](../xml-tools/searching-the-schema-set.md).  
  
- Adicionar os resultados de pesquisa à Exibição de Gráfico ou Exibição de Modelo de Conteúdo  
  
- Classificar a árvore pela ordem de documento, tipo ou nome. Para obter mais informações, consulte [classificação, filtragem e agrupamento](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md).  
  
- Abra o Editor de XML e pule para as localizações de código no arquivo XSD. Para obter mais informações, consulte [integração com Editor XML](../xml-tools/integration-with-xml-editor.md).  
  
- Gere o exemplo de XML para elementos globais.  
  
  O XML Schema Explorer fornece uma exibição hierárquica do conjunto de esquema por meio de uma exibição de árvore. O XML Schema Explorer também fornece pesquisa, filtragem, navegação e classificação. Para acessar o XML Schema Explorer, faça o seguinte:  
  
- Se você estiver usando o [iniciar o modo de exibição](../xml-tools/start-view.md), clique no **XML Schema Explorer** link.  
  
- Se você estiver usando o [exibição de gráfico](../xml-tools/graph-view.md) ou o [exibição de modelo de conteúdo](../xml-tools/content-model-view.md) e tiver nós em seu espaço de trabalho, use o menu de contexto para selecionar o XML Schema Explorer.  
  
- Você também pode selecionar o Explorerfrom de esquema XML o **exibição** menu.  
  
- Você pode acessar o Explorerfrom de esquema XML um arquivo. vb que tem um literal de XML de Visual Basic associado a um arquivo. xsd. Para ver o esquema definido em XML Schema Explorer, clique com botão direito um nó XML em um literal XML ou uma importação de namespace XML e selecione o **Mostrar no Schema Explorer** comando. Para obter mais informações, consulte [integração de literais XML com XML Schema Explorer](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md).  
  
## <a name="tree-view"></a>Exibição de árvore  
 O XML Schema Explorer exibe informações de conjunto de esquema pré-compilado em uma estrutura de árvore. A estrutura de árvore é organizada da seguinte maneira:  
  
- No nível superior está o nó do conjunto de esquema.  
  
- O segundo nível contém os namespaces.  
  
- O terceiro nível contém os arquivos.  
  
- O quarto nível contém os nós globais. Isso pode incluir elementos, grupos, tipos complexos, tipos simples, atributos, grupos de atributo e instruções `include`, `import` e `redefine`.  
  
  A seguir veja um exemplo de uma estrutura de árvore:  
  
  ![XML Schema Explorer](../xml-tools/media/xmlschemaexplorer.gif "XMLSchemaExplorer")  
  
## <a name="selection-and-activation"></a>Seleção e ativação  
 Para realçar e selecionar um nó, clique uma vez no Schema Explorer.  
  
 Para ativar um nó, clique duas vezes nele ou pressione **Enter** quando o nó é selecionado.  
  
-   Ativar um nó abre o arquivo no qual o nó está definido (se o arquivo já não estiver aberto) e seleciona o nó no arquivo.  
  
-   Ativar um nó de arquivo abre o arquivo selecionado (se ele já não estiver aberto) e destaca o nó `<schema>`.  
  
-   Ativar um SchemaSet ou um nó de namespace não fará nada.  
  
## <a name="draging-and-dropping-nodes"></a>Nós de arrastar e soltar  
 Você pode arrastar e soltar nós globais, nós de arquivo e nós de namespace em uma exibição do Designer XSD. Se a exibição atual for o [iniciar o modo de exibição](../xml-tools/start-view.md), arrastar um nó para o modo de exibição será aberto o [modo de exibição gráfico](../xml-tools/graph-view.md). Se a exibição atual for o [modo de exibição do modelo de conteúdo](../xml-tools/content-model-view.md) ou modo de exibição de gráfico, o modo de exibição não será alterado quando você remove um nó nela.  
  
 Soltar arquivos na exibição adicionará todos os nós globais no arquivo para o [espaço de trabalho do Designer XSD](../xml-tools/xml-schema-designer-workspace.md). Soltar namespaces na exibição adicionará todos os nós globais no namespace para o workspace. O workspace é compartilhado entre todas as visualizações.  
  
 Você não pode arrastar e soltar nós locais ou importações.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Pesquisando pelo conjunto de esquema](../xml-tools/searching-the-schema-set.md)  
  
-   [Classificação, filtragem e agrupamento](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)  
  
-   [Menus de contexto](../xml-tools/context-menus-xml-schema-explorer.md)  
  
-   [Integração de literais XML com XML Schema Explorer](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como adicionar nós ao workspace por meio do XML Schema Explorer](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)







