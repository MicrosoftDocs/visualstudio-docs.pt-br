---
title: 'Como: imprimir planilhas programaticamente'
description: Saiba como você pode usar o Visual Studio para imprimir programaticamente qualquer planilha em uma pasta de trabalho do Microsoft Excel.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 129493f726967776aa669eb92f6e912ed9c1b11b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827143"
---
# <a name="how-to-programmatically-print-worksheets"></a>Como: imprimir planilhas programaticamente

Você pode imprimir qualquer planilha em uma pasta de trabalho.

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>Imprimir uma planilha em uma personalização no nível do documento

### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha

1. Chame o `PrintOut` método de `Sheet1` , solicite duas cópias e visualize o documento antes de imprimir.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet22":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet22":::

   O <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado na janela de **visualização de impressão** . O código a seguir pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host chamado `Sheet1` .

### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes da impressão

1. Chame o <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método da planilha.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet23":::

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>Imprimir uma planilha em um suplemento do VSTO

### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> método da planilha ativa, solicite duas cópias e visualize o documento antes de imprimir.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet14":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet14":::

   O <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado na janela de **visualização de impressão** .

### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes da impressão

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método da planilha ativa.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>Consulte também

- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: verificar a ortografia em planilhas programaticamente](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [Item de host de planilha](../vsto/worksheet-host-item.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
