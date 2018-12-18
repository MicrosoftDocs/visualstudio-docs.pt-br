---
title: 'Como: adicionar novas planilhas a pastas de trabalho programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, adding worksheets
- workbooks, creating worksheets
- worksheets, creating
- worksheets, adding to workbooks
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 80e3ddaa3edd4520e16c8733d3310497ab4ea5af
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255005"
---
# <a name="how-to-programmatically-add-new-worksheets-to-workbooks"></a>Como: adicionar novas planilhas a pastas de trabalho programaticamente
  Você pode criar programaticamente uma planilha e, em seguida, adicionar a planilha para a coleção de planilhas na pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-document-level-customization"></a>Para adicionar uma nova planilha para uma pasta de trabalho em uma personalização no nível de documento  
  
1.  Use o <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#15](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomation#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#15)]  
  
     A nova planilha é um nativo <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto e não um item de host. Se você quiser adicionar um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host, você deve adicionar a planilha em tempo de design.  
  
## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-vsto-add-in"></a>Para adicionar uma nova planilha para uma pasta de trabalho em um suplemento do VSTO  
  
1.  Use o <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#11](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#11](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#11)]  
  
     A nova planilha é um nativo <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto e não um item de host. Você também pode gerar uma <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host do nativo <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto. Para obter mais informações, consulte [Estendendo documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Como: excluir planilhas de pastas de trabalho de forma programática](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)   
 [Como: Selecionar planilhas programaticamente](../vsto/how-to-programmatically-select-worksheets.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  