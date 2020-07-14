---
title: 'Como: Adicionar e excluir de forma programática comentários da planilha'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, comments
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: dc02a659c50a5b207f2f53d0a8781b0d23419301
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520075"
---
# <a name="how-to-programmatically-add-and-delete-worksheet-comments"></a>Como: Adicionar e excluir de forma programática comentários da planilha
  Você pode adicionar e excluir de forma programática comentários em Microsoft Office planilhas do Excel. Os comentários podem ser adicionados somente a células únicas, não a intervalos com várias células.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="add-and-delete-a-comment-in-a-document-level-project"></a>Adicionar e excluir um comentário em um projeto de nível de documento
 Os exemplos a seguir pressupõem que há um controle de célula única <xref:Microsoft.Office.Tools.Excel.NamedRange> chamado `dateComment` em uma planilha chamada `Sheet1` .

### <a name="to-add-a-new-comment-to-a-named-range"></a>Para adicionar um novo comentário a um intervalo nomeado

1. Chame o <xref:Microsoft.Office.Tools.Excel.NamedRange.AddComment%2A> método do <xref:Microsoft.Office.Tools.Excel.NamedRange> controle e forneça o texto do comentário. Esse código deve ser colocado na `Sheet1` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#30](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#30)]
     [!code-vb[Trin_VstcoreExcelAutomation#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#30)]

#### <a name="to-delete-a-comment-from-a-named-range"></a>Para excluir um comentário de um intervalo nomeado

1. Verifique se existe um comentário no intervalo e exclua-o. Esse código deve ser colocado na `Sheet1` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#29](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#29)]
     [!code-vb[Trin_VstcoreExcelAutomation#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#29)]

## <a name="add-and-delete-a-comment-in-a-vsto-add-in-project"></a>Adicionar e excluir um comentário em um projeto de suplemento do VSTO
 Os exemplos a seguir pressupõem que haja uma única célula <xref:Microsoft.Office.Interop.Excel.Range> chamada `dateComment` na planilha ativa.

### <a name="to-add-a-new-comment-to-an-excel-range"></a>Para adicionar um novo comentário a um intervalo do Excel

1. Chame o <xref:Microsoft.Office.Interop.Excel.Range.AddComment%2A> método do <xref:Microsoft.Office.Interop.Excel.Range> e forneça o texto do comentário.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#20](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#20)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#20](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#20)]

### <a name="to-delete-a-comment-from-an-excel-range"></a>Para excluir um comentário de um intervalo do Excel

1. Verifique se existe um comentário no intervalo e exclua-o.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#19](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#19)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#19](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#19)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como exibir programaticamente comentários de planilha](../vsto/how-to-programmatically-display-worksheet-comments.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
