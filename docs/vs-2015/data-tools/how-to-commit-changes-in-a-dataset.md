---
title: 'Como: Confirmar alterações em um conjunto de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- DataSet.AcceptChanges
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- datasets [Visual Basic], committing changes
ms.assetid: 51931353-4d22-4e35-a9ef-6f2b44e1f7d9
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 41d27c248763f42db6543db0a9b4e56e4c4eac82
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49276426"
---
# <a name="how-to-commit-changes-in-a-dataset"></a>Como confirmar alterações em um conjunto de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Conforme você faz alterações a registros em um conjunto de dados, atualizar, inserir e excluindo registros, o conjunto de dados mantém versões originais e atuais dos registros. Além disso, cada linha <xref:System.Data.DataRow.RowState%2A> propriedade mantém o controle de se os registros estão em seu estado original ou tiveram sido atualizados, inseridos ou excluídos. Essas informações são úteis quando você precisa encontrar uma versão específica de uma linha. Normalmente, você obteria um subconjunto de todos os registros modificados para enviar para outro processo. Para obter mais informações, consulte [como: recuperar linhas alteradas](http://msdn.microsoft.com/library/6ff0cbd0-5253-48e7-888a-144d56c2e0a9). Depois que tiver processado todas as linhas alteradas, você pode confirmar as alterações chamando o `AcceptChanges` método da <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, ou <xref:System.Data.DataRow>. O `AcceptChanges` método é chamado automaticamente ao chamar os métodos de atualização de um [TableAdapter](../data-tools/tableadapter-overview.md) ou adaptador de dados. Chamar `AcceptChanges` após enviar alterações para um banco de dados.  
  
 Quando você chama <xref:System.Data.DataSet.AcceptChanges%2A> sobre o <xref:System.Data.DataSet>, qualquer <xref:System.Data.DataRow> objetos ainda no modo de edição terminam com êxito suas edições. O <xref:System.Data.DataRow.RowState%2A> propriedade de cada <xref:System.Data.DataRow> também muda; <xref:System.Data.DataRowState> e <xref:System.Data.DataRowState> linhas se tornam <xref:System.Data.DataRowState>, e <xref:System.Data.DataRowState> linhas são removidas.  
  
 Se o <xref:System.Data.DataSet> contém <xref:System.Data.ForeignKeyConstraint> objetos, invocando o <xref:System.Data.DataSet.AcceptChanges%2A> método também faz com que o <xref:System.Data.AcceptRejectRule> seja imposta.  
  
### <a name="to-commit-changes-in-a-dataset"></a>Para confirmar as alterações em um conjunto de dados  
  
-   Chame o `AcceptChanges` método quanto um <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, ou <xref:System.Data.DataRow> para confirmar as alterações nesses objetos.  
  
     O exemplo a seguir mostra como chamar o `AcceptChanges` método para confirmar as alterações no `Customers` tabela depois de atualizar uma fonte de dados:  
  
     [!code-csharp[VbRaddataEditing#11](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#11)]
     [!code-vb[VbRaddataEditing#11](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#11)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>   
 <xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>   
 <xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>   
 [Salvando dados](../data-tools/saving-data.md)   
 [Como: recuperar linhas alteradas](http://msdn.microsoft.com/library/6ff0cbd0-5253-48e7-888a-144d56c2e0a9)