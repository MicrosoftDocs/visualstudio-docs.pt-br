---
title: 'Como: obter versões específicas de um DataRow | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- row states
- updating datasets, row states
- DataRow object
ms.assetid: d7cde25e-cef5-4559-b994-be00e258ac1f
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 5bd8ae12c77c671e375043a0381a4b580d1a03d7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49255476"
---
# <a name="how-to-get-specific-versions-of-a-datarow"></a>Como obter versões específicas de um DataRow
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando forem feitas alterações a linhas de dados, o conjunto de dados manterá tanto o original (<xref:System.Data.DataRowVersion>) e new (<xref:System.Data.DataRowVersion>) versões da linha. Por exemplo, antes de chamar o `AcceptChanges` método, seu aplicativo pode acessar as versões diferentes de um registro (conforme definido no <xref:System.Data.DataRowVersion> enumeração) e processar as alterações de acordo.  
  
> [!NOTE]
>  Versões diferentes de uma linha existem somente após ele ter sido editado e antes que tenha tido o `AcceptChanges` método chamado. Após o `AcceptChanges` método foi chamado, as versões atuais e originais são as mesmas.  
  
 Passando o <xref:System.Data.DataRowVersion> valor juntamente com o índice da coluna (ou o nome da coluna como uma cadeia de caracteres) retorna o valor da versão de linha específica da coluna. A coluna alterada é identificada durante o <xref:System.Data.DataTable.ColumnChanging> e <xref:System.Data.DataTable.ColumnChanged> versões para fins de validação de linha de eventos, portanto, que é um bom momento para inspecionar a diferença. No entanto, se você tiver temporariamente as restrições suspensas, esses eventos não serão gerados e você precisará identificar programaticamente quais colunas foram alteradas. Você pode fazer isso ao iterar por meio de <xref:System.Data.DataTable.Columns%2A> coleta e comparar as diferentes <xref:System.Data.DataRowVersion> valores.  
  
## <a name="accessing-the-original-version-of-a-datarow"></a>Acessando a versão Original de uma DataRow  
  
#### <a name="to-get-the-original-version-of-a-record"></a>Para obter a versão original de um registro  
  
-   Acessar o valor de uma coluna passando o <xref:System.Data.DataRowVersion> da linha que você deseja retornar.  
  
     O exemplo a seguir mostra como você pode usar um <xref:System.Data.DataRowVersion> valor para obter o valor original de um `CompanyName` campo em um <xref:System.Data.DataRow>:  
  
     [!code-csharp[VbRaddataEditing#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#21)]
     [!code-vb[VbRaddataEditing#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#21)]  
  
## <a name="accessing-the-current-version-of-a-datarow"></a>Acessando a versão atual de um DataRow  
  
#### <a name="to-get-the-current-version-of-a-record"></a>Para obter a versão atual de um registro  
  
-   Acessar o valor de uma coluna e adicione um parâmetro para o índice que indica qual versão de uma linha que você deseja retornar.  
  
     O exemplo a seguir mostra como você pode usar um <xref:System.Data.DataRowVersion> valor para obter o valor atual de um `CompanyName` campo em um <xref:System.Data.DataRow>:  
  
     [!code-csharp[VbRaddataEditing#22](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#22)]
     [!code-vb[VbRaddataEditing#22](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#22)]  
  
## <a name="see-also"></a>Consulte também  
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)