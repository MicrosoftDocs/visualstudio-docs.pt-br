---
title: Adicionar nós ao espaço de trabalho do XML Schema Explorer
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 751e291188e6357343936d61d56f07bd86f97eaf
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816391"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>Como adicionar nós ao espaço de trabalho do XML Schema Explorer

Este tópico explica como adicionar nós ao espaço de [trabalho do designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md) do **XML Schema Explorer**. Isso pode ser obtido arrastando e soltando nós do **XML Schema Explorer** em uma exibição de designer xsd ou usando o menu de contexto **do XML Schema Explorer** . Você também pode adicionar nós que são realçados como resultado de uma pesquisa realizada pelo **XML Schema Explorer**. Para obter mais informações, consulte [como adicionar nós de resultado de pesquisa de conjunto de esquema ao espaço de trabalho](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md).

> [!NOTE]
> Somente nós globais podem ser adicionados ao [espaço de trabalho do designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md).

## <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>Para adicionar nós por meio do menu de contexto do Gerenciador de XML

1. Siga as etapas em [como criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).

2. Clique com o botão direito do mouse no `PurchaseOrderType` nó no Gerenciador de XSD. Selecione **Mostrar no modo de exibição de gráfico**.

     O nó de `purchaseOrderType` aparece na superfície de design do modo de gráfico.

## <a name="to-drag-and-drop-a-node-on-to-a-view"></a>Para arrastar e soltar sobre um nó para uma visualização

1. Clique com o botão direito do mouse no `PurchaseOrderType` nó no modo de exibição de gráfico. Selecione **Mostrar no Gerenciador de esquema XML**.

     O nó é realçado no **XML Schema Explorer**.

2. Clique com o botão direito do mouse no `PurchaseOrderType` nó no **XML Schema Explorer** e selecione **Mostrar todas as referências**.

     O nó de `purchaseOrder` é realçado.

3. Arraste o nó de `purchaseOrder` sobre para o modo de exibição gráfico.

     O nó de `purchaseOrder` e o nó de `PurchaseOrderType` aparecem próximos uns dos outros na superfície de design do modo de gráfico. Porque os dois nós são relacionados (o elemento de `purchaseOrder` é do tipo de `PurchaseOrderType` ), uma seta é desenhada entre eles.

## <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>Para adicionar nós que usam o esquema Explorer pesquisam o recurso

1. Digite "purchaseOrder" na caixa de texto Pesquisar da barra de ferramentas do [Gerenciador de XML](../xml-tools/xml-schema-explorer.md) e clique no botão Pesquisar.

     ![Pesquisa de palavra-chave do XML Schema Explorer](../xml-tools/media/schemaexplorersearch.gif)

     Os resultados da pesquisa são realçados no **XML Schema Explorer** e marcados por tiques na barra de rolagem vertical.

2. Adicione os resultados da pesquisa ao espaço de trabalho clicando no botão **adicionar nós realçados ao espaço de trabalho** no painel resultados do resumo.

     ![Resultado da pesquisa do XML Schema Explorer](../xml-tools/media/schemaexplorersearchresult.gif)

     O `purchaseOrder` nó e o `PurchaseOrderType` nó aparecem ao lado um do outro na superfície de design do [modo de exibição de gráfico](../xml-tools/graph-view.md). Porque os dois nós são relacionados (o elemento de `purchaseOrder` é do tipo de `PurchaseOrderType` ), uma seta é desenhada entre eles.

## <a name="see-also"></a>Veja também

- [XML Schema Explorer](../xml-tools/xml-schema-explorer.md)
