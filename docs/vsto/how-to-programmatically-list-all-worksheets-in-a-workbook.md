---
title: 'Como: listar programaticamente todas as planilhas em uma pasta de trabalho'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing worksheets
- worksheets, listing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bb82b26fedce0590c5c2fe9cfa1b321fef5dbf19
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257755"
---
# <a name="how-to-programmatically-list-all-worksheets-in-a-workbook"></a>Como: listar programaticamente todas as planilhas em uma pasta de trabalho
  O <xref:Microsoft.Office.Interop.Excel.Workbook> classe fornece um <xref:Microsoft.Office.Interop.Excel.Worksheets> objeto. Este objeto contém uma coleção de todos os <xref:Microsoft.Office.Interop.Excel.Worksheet> objetos na pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-document-level-customization"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em uma personalização no nível de documento  
  
1.  Iterar por meio de <xref:Microsoft.Office.Interop.Excel.Worksheets> coleta e envie o nome de cada folha a uma célula de deslocamento de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#21)]
     [!code-vb[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#21)]  
  
## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-vsto-add-in"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em um suplemento do VSTO  
  
1.  Iterar por meio de <xref:Microsoft.Office.Interop.Excel.Worksheets> coleta e envie o nome de cada folha a uma célula de deslocamento de um <xref:Microsoft.Office.Interop.Excel.Range> objeto.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#13)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#13)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: adicionar novas planilhas a pastas de trabalho programaticamente](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)   
 [Como: mover planilhas em pastas de trabalho de forma programática](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)  
  
  