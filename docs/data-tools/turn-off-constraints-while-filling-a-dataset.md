---
title: Desabilitar restrições ao preencher um conjunto de dados
description: Saiba como desativar restrições ao preencher um conjunto de um DataSet. Suspenda as restrições de atualização programaticamente ou usando o Designer de Conjunto de Dados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 3280894ba1634f9775def74a88dcb413c94ba77a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215702"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>Desabilitar restrições ao preencher um conjunto de dados

Se um conjunto de um dataset contiver restrições (como restrições Foreign-Key), eles poderão gerar erros relacionados à ordem das operações executadas no conjunto de um. Por exemplo, carregar registros filho antes de carregar registros pai relacionados pode violar uma restrição e causar um erro. Assim que você carregar um registro filho, a restrição verificará o registro pai relacionado e gerará um erro.

Se não houver nenhum mecanismo para permitir a suspensão de restrição temporária, um erro será gerado toda vez que você tentar carregar um registro na tabela filho. Outra maneira de suspender todas as restrições em um conjunto de um DataSet é com as <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataRow.EndEdit%2A> Propriedades e.

> [!NOTE]
> Eventos de validação (por exemplo, <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> ) não serão gerados quando as restrições forem desativadas.

## <a name="to-suspend-update-constraints-programmatically"></a>Para suspender restrições de atualização programaticamente

- O exemplo a seguir mostra como desativar temporariamente a verificação de restrição em um conjunto de uma:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet10":::

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>Para suspender restrições de atualização usando o Designer de Conjunto de Dados

1. Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. Na janela **Propriedades** , defina a <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade como `false` .

## <a name="see-also"></a>Confira também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)
- [Relacionamentos em conjuntos de dados](../data-tools/relationships-in-datasets.md)
