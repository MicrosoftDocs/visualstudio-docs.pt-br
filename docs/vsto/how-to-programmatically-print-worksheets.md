---
title: 'Como: Imprimir programaticamente planilhas'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 764723d0749cd82739d8e67ee71104f41a0f9065
ms.sourcegitcommit: 5b34052a1c7d86179d7898ed532babb2d9dad4a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69490591"
---
# <a name="how-to-programmatically-print-worksheets"></a>Como: Imprimir programaticamente planilhas

Você pode imprimir qualquer planilha em uma pasta de trabalho.

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>Imprimir uma planilha em uma personalização no nível do documento

### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha

1. Chame o `PrintOut` método de `Sheet1`, solicite duas cópias e visualize o documento antes de imprimir.

    [!code-csharp[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#22)]
    [!code-vb[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#22)]

   O <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado na janela de **visualização de impressão** . O código a seguir pressupõe que você <xref:Microsoft.Office.Tools.Excel.Worksheet> tenha um item `Sheet1`de host chamado.

### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes da impressão

1. Chame o <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método da planilha.

     [!code-csharp[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#23)]

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>Imprimir uma planilha em um suplemento do VSTO

### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> método da planilha ativa, solicite duas cópias e visualize o documento antes de imprimir.

    [!code-csharp[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#14)]
    [!code-vb[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#14)]

   O <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado na janela de **visualização de impressão** .

### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes da impressão

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método da planilha ativa.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#15)]

## <a name="see-also"></a>Consulte também

- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: Verificar programaticamente a ortografia em planilhas](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [Item de host de planilha](../vsto/worksheet-host-item.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
