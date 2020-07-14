---
title: 'Como: agrupar linhas programaticamente em uma planilha'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 759ba8c6e0796b25a87e8bf0b08795aed5bade05
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537872"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>Como: agrupar linhas programaticamente em uma planilha
  Você pode agrupar uma ou mais linhas inteiras. Para criar um grupo em uma planilha, use um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou um objeto Range do Excel nativo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange
 Se você adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a um projeto de nível de documento no tempo de design, poderá usar o controle para criar programaticamente um grupo. O exemplo a seguir pressupõe que há três <xref:Microsoft.Office.Tools.Excel.NamedRange> controles na mesma planilha: `data2001` , `data2002` e `dataAll` . Cada intervalo nomeado refere-se a uma linha inteira na planilha.

### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>Para criar um grupo de controles NamedRange em uma planilha

1. Agrupe três intervalos nomeados chamando o <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> método de cada intervalo. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]

    > [!NOTE]
    > Para desagrupar linhas, chame o <xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> método.

## <a name="use-native-excel-ranges"></a>Usar intervalos nativos do Excel
 O código pressupõe que você tenha três intervalos do Excel denominados `data2001` , `data2002` e `dataAll` em uma planilha.

### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>Para criar um grupo de intervalos do Excel em uma planilha

1. Agrupe três intervalos nomeados chamando o <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> método de cada intervalo. O exemplo a seguir pressupõe que há três <xref:Microsoft.Office.Interop.Excel.Range> controles chamados `data2001` , `data2002` e `dataAll` na mesma planilha. Cada intervalo nomeado refere-se a uma linha inteira na planilha.

     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]

    > [!NOTE]
    > Para desagrupar linhas, chame o <xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> método.

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
