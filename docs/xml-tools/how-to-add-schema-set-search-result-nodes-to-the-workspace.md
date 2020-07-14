---
title: Adicionar nós de resultados de pesquisa do conjunto de esquema XML ao espaço de trabalho
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d94544fd017809b32b7a144b16da4515e6b2e4bb
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816313"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>Como adicionar nós de resultado de pesquisa de conjunto de esquema ao espaço de trabalho

Este tópico explica como adicionar nós que são realçados no **XML Schema Explorer** como o resultado de uma pesquisa de palavra-chave no espaço de trabalho.

> [!NOTE]
> Somente nós globais podem ser adicionados ao [espaço de trabalho](../xml-tools/xml-schema-designer-workspace.md).

Este exemplo usa o [esquema de ordem de compra](../xml-tools/sample-xsd-file-purchase-order-schema.md)de exemplo.

## <a name="to-add-schema-set-result-nodes"></a>Para adicionar nós definidos do resultado de esquema

1. Siga as etapas em [como criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).

2. Digite "purchaseOrder" na caixa de texto Pesquisar da barra de ferramentas do [Gerenciador de XML](../xml-tools/xml-schema-explorer.md) e clique no botão Pesquisar.

     ![Pesquisa de palavra-chave do XML Schema Explorer](../xml-tools/media/schemaexplorersearch.gif)

     Os resultados da pesquisa são realçados no **XML Schema Explorer** e marcados por tiques na barra de rolagem vertical.

3. Adicione os resultados da pesquisa ao espaço de trabalho clicando no botão **adicionar nós realçados ao espaço de trabalho** no painel resultados do resumo.

     ![Resultado da pesquisa do XML Schema Explorer](../xml-tools/media/schemaexplorersearchresult.gif)

     O `purchaseOrder` nó e o `PurchaseOrderType` nó aparecem ao lado um do outro na superfície de design do [modo de exibição de gráfico](../xml-tools/graph-view.md). Porque os dois nós são relacionados (o elemento de `purchaseOrder` é do tipo de `PurchaseOrderType` ), uma seta é desenhada entre eles.
