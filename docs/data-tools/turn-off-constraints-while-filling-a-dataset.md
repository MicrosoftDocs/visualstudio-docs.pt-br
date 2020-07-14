---
title: Desabilitar restrições ao preencher um conjunto de dados
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
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 7bdb225a5b310f6f602619b2afcee610c3e9258b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281260"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>Desabilitar restrições ao preencher um conjunto de dados

Se um conjunto de um dataset contiver restrições (como restrições Foreign-Key), eles poderão gerar erros relacionados à ordem das operações executadas no conjunto de um. Por exemplo, carregar registros filho antes de carregar registros pai relacionados pode violar uma restrição e causar um erro. Assim que você carregar um registro filho, a restrição verificará o registro pai relacionado e gerará um erro.

Se não houver nenhum mecanismo para permitir a suspensão de restrição temporária, um erro será gerado toda vez que você tentar carregar um registro na tabela filho. Outra maneira de suspender todas as restrições em um conjunto de um DataSet é com as <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataRow.EndEdit%2A> Propriedades e.

> [!NOTE]
> Eventos de validação (por exemplo, <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.RowChanging> ) não serão gerados quando as restrições forem desativadas.

## <a name="to-suspend-update-constraints-programmatically"></a>Para suspender restrições de atualização programaticamente

- O exemplo a seguir mostra como desativar temporariamente a verificação de restrição em um conjunto de uma:

     [!code-csharp[VbRaddataEditing#10](../data-tools/codesnippet/CSharp/turn-off-constraints-while-filling-a-dataset_1.cs)]
     [!code-vb[VbRaddataEditing#10](../data-tools/codesnippet/VisualBasic/turn-off-constraints-while-filling-a-dataset_1.vb)]

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>Para suspender restrições de atualização usando o Designer de Conjunto de Dados

1. Abra o conjunto de dados no **Designer de Conjunto de Dados**. Para obter mais informações, consulte [Walkthrough: Criando um conjunto de dados no designer de conjunto de dados](walkthrough-creating-a-dataset-with-the-dataset-designer.md).

2. Na janela **Propriedades** , defina a <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade como `false` .

## <a name="see-also"></a>Veja também

- [Preencher conjuntos de dados usando TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)
- [Relacionamentos em conjuntos de dados](../data-tools/relationships-in-datasets.md)
