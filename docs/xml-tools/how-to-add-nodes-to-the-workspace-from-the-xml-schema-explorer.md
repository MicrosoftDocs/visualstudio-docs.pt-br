---
title: 'Como: Adicionar nós ao espaço de trabalho XML Schema Explorer'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3e1f5821d3a4207d89eb62b9344cff967c73b536
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752047"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>Como: adicionar nós ao espaço de trabalho do Gerenciador de esquema XML

Este tópico explica como adicionar nós a [espaço de trabalho do Designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md) do **XML Schema Explorer**. Isso pode ser feito arrastando e soltando nós do **XML Schema Explorer** em uma exibição de Designer de XSD ou usando o **XML Schema Explorer** menu de contexto. Você também pode adicionar nós realçados como resultado de uma pesquisa executada pelo **XML Schema Explorer**. Para obter mais informações, consulte [como: adicionar nós de resultados de pesquisa de conjunto de esquema para o espaço de trabalho](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md).

> [!NOTE]
> Somente nós globais podem ser adicionados para o [espaço de trabalho do Designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md).

## <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>Para adicionar nós por meio do menu de contexto do Gerenciador de XML

1.  Siga as etapas em [como: criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).

2.  Clique com o botão direito no `PurchaseOrderType` nó no Gerenciador de XSD. Selecione **Mostrar na exibição de gráfico**.

     O nó de `purchaseOrderType` aparece na superfície de design do modo de gráfico.

## <a name="to-drag-and-drop-a-node-on-to-a-view"></a>Para arrastar e soltar sobre um nó para uma visualização

1.  Clique com botão direito no `PurchaseOrderType` nó no modo de exibição de gráfico. Selecione **Mostrar em XML Schema Explorer**.

     O nó é realçado no **XML Schema Explorer**.

2.  Clique com o botão direito no `PurchaseOrderType` nó o **XML Schema Explorer** e selecione **Mostrar todas as referências**.

     O nó de `purchaseOrder` é realçado.

3.  Arraste o nó de `purchaseOrder` sobre para o modo de exibição gráfico.

     O nó de `purchaseOrder` e o nó de `PurchaseOrderType` aparecem próximos uns dos outros na superfície de design do modo de gráfico. Porque os dois nós são relacionados (o elemento de `purchaseOrder` é do tipo de `PurchaseOrderType` ), uma seta é desenhada entre eles.

## <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>Para adicionar nós que usam o esquema Explorer pesquisam o recurso

1.  Digite "purchaseOrder" na caixa de texto de pesquisa do [XML Explorer](../xml-tools/xml-schema-explorer.md) barra de ferramentas e clique no botão de pesquisa.

     ![Pesquisa de palavra-chave do XML Schema Explorer](../xml-tools/media/schemaexplorersearch.gif)

     Os resultados da pesquisa são realçados no **XML Schema Explorer** e marcado pelo tiques na barra de rolagem vertical.

2.  Adicionar os resultados da pesquisa para o espaço de trabalho clicando o **adicionar nós realçados ao espaço de trabalho** botão no painel de resultados de resumo.

     ![Resultado da pesquisa do XML Schema Explorer](../xml-tools/media/schemaexplorersearchresult.gif)

     O `purchaseOrder` nó e o `PurchaseOrderType` nó aparecer ao lado do outro na superfície de design do [exibição de gráfico](../xml-tools/graph-view.md). Porque os dois nós são relacionados (o elemento de `purchaseOrder` é do tipo de `PurchaseOrderType` ), uma seta é desenhada entre eles.

## <a name="see-also"></a>Consulte também

- [XML Schema Explorer](../xml-tools/xml-schema-explorer.md)