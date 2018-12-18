---
title: XML Schema Explorer
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 110cad9883cbb129368dac4d481443a9f5d9813c
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34751583"
---
# <a name="xml-schema-explorer"></a>XML Schema Explorer

O **XML Schema Explorer** é integrado com o Microsoft Visual Studio e o Editor de XML para que você possa trabalhar com esquemas de linguagem XSD de definição de esquema XML. Quando você abre um arquivo de esquema XML, o **esquema definido** nó aparece no **XML Schema Explorer**. Todos os esquemas de incluído, importados ou redefinidos para seu arquivo de destino, bem como todos os arquivos que são referenciados por meio de um `include` ou `import` instrução, também aparecem no **XML Schema Explorer**.

 O **XML Schema Explorer** permite que você faça o seguinte:

-   Obter uma visão geral rápido do conjunto de esquema.

-   Procurar e navegar na árvore.

-   Realizar pesquisas de palavra-chave e específicas do esquema. Para obter mais informações, consulte [pesquisando o conjunto de esquema](../xml-tools/searching-the-schema-set.md).

-   Adicionar os resultados da pesquisa para a exibição de gráfico ou a exibição do modelo de conteúdo

-   Classificar a árvore pela ordem de documento, tipo ou nome. Para obter mais informações, consulte [classificação, filtragem e agrupamento](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md).

-   Abra o Editor de XML e pule para as localizações de código no arquivo XSD. Para obter mais informações, consulte [integração com o Editor de XML](../xml-tools/integration-with-xml-editor.md).

-   Gere o exemplo de XML para elementos globais.

O **XML Schema Explorer** fornece uma exibição hierárquica do esquema definido por meio de uma exibição de árvore. O **XML Schema Explorer** também fornece pesquisa, filtragem, navegação e classificação. Para acessar o **XML Schema Explorer**, faça o seguinte:

-   Se você estiver usando o [exibição início](../xml-tools/start-view.md), clique no **XML Schema Explorer** link.

-   Se você estiver usando o [exibição de gráfico](../xml-tools/graph-view.md) ou [exibição do modelo de conteúdo](../xml-tools/content-model-view.md) e ter nós em seu espaço de trabalho, use o menu de contexto para selecionar o **XML Schema Explorer**.

-   Você também pode selecionar o **XML Schema Explorer** do **exibição** menu.

-   Você pode acessar o **XML Schema Explorer** de um *. vb* arquivo que tenha um literal de XML do Visual Basic associado com um *. xsd* arquivo. Para ver o esquema definido **XML Schema Explorer**, um nó XML em um literal XML ou uma importação de namespace XML e selecione o **Mostrar no Gerenciador de esquema** comando. Para obter mais informações, consulte [literais de integração de XML com XML Schema Explorer](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md).

## <a name="tree-view"></a>Exibição de árvore
 O **XML Schema Explorer** exibe pré-compilado esquema configurar informações em uma estrutura de árvore. A estrutura de árvore é organizada da seguinte maneira:

-   No nível superior está o nó do conjunto de esquema.

-   O segundo nível contém os namespaces.

-   O terceiro nível contém os arquivos.

-   O quarto nível contém os nós globais. Isso pode incluir elementos, grupos, tipos complexos, tipos simples, atributos, grupos de atributo e instruções `include`, `import` e `redefine`.

A seguir veja um exemplo de uma estrutura de árvore:

![XML Schema Explorer](../xml-tools/media/xmlschemaexplorer.gif)

## <a name="selection-and-activation"></a>Seleção e ativação
 Para realçar e selecionar um nó, clique uma vez no Schema Explorer.

 Para ativar um nó, clique duas vezes ou pressione **Enter** quando o nó é selecionado.

-   Ativar um nó abre o arquivo no qual o nó está definido (se o arquivo já não estiver aberto) e seleciona o nó no arquivo.

-   Ativar um nó de arquivo abre o arquivo selecionado (se ele já não estiver aberto) e destaca o nó `<schema>`.

-   Ativar um SchemaSet ou um nó de namespace não fará nada.

## <a name="drag-and-drop-nodes"></a>Arraste e solte os nós
 Você pode arrastar e soltar nós globais, nós de arquivo e nós de namespace em uma exibição do Designer XSD. Se o modo de exibição atual for a [exibição início](../xml-tools/start-view.md), arrastar um nó para o modo de exibição será aberto a [exibição de gráfico](../xml-tools/graph-view.md). Se o modo de exibição atual for a [exibição do modelo de conteúdo](../xml-tools/content-model-view.md) ou modo de exibição de gráfico, o modo de exibição não será alterado quando você remover um nó para ele.

 Remover arquivos no modo de exibição adicionará todos os nós global no arquivo para o [espaço de trabalho do Designer de XSD](../xml-tools/xml-schema-designer-workspace.md). Soltar namespaces na exibição adicionará todos os nós globais no namespace para o espaço de trabalho. O espaço de trabalho é compartilhado entre todas as visualizações.

 Você não pode arrastar e soltar nós locais ou importações.

## <a name="see-also"></a>Consulte também

- [Como: adicionar nós ao espaço de trabalho do Gerenciador de esquema XML](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)