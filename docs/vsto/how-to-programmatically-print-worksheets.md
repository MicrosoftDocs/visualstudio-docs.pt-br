---
title: 'Como: Imprimir planilhas programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c1e473baccd6e4bb4de1c36d8888082baf40034b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49876629"
---
# <a name="how-to-programmatically-print-worksheets"></a>Como: Imprimir planilhas programaticamente
  Você pode imprimir qualquer planilha em uma pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="print-a-worksheet-in-a-document-level-customization"></a>Imprimir uma planilha em uma personalização no nível de documento  
  
### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha  
  
1. Chame o <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintOut%2A> método de `Sheet1`, duas cópias de solicitação e visualizar o documento antes de imprimir.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#22)]
    [!code-vb[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#22)]  
  
   O <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado em de **Visualizar impressão** janela. O código a seguir pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host chamado `Sheet1`.  
  
### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes de imprimir  
  
1.  Chamar o <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> método da planilha.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#23)]  
  
## <a name="print-a-worksheet-in-a-vsto-add-in"></a>Imprimir uma planilha em um suplemento do VSTO  
  
### <a name="to-print-a-worksheet"></a>Para imprimir uma planilha  
  
1. Chamar o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> método da planilha ativa, duas cópias de solicitação e visualizar o documento antes de imprimir.  
  
    [!code-csharp[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#14)]
    [!code-vb[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#14)]  
  
   O <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método permite que você exiba o objeto especificado em de **Visualizar impressão** janela.  
  
### <a name="to-preview-a-page-before-printing"></a>Para visualizar uma página antes de imprimir  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> método da planilha ativa.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#15)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: verificar a ortografia em planilhas de forma programática](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)   
 [Item de host da planilha](../vsto/worksheet-host-item.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  