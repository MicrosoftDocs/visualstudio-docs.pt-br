---
title: 'Como: copiar planilhas programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying
- Excel [Office development in Visual Studio], copying worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8226f337994c686d4d370e91831bc1262d3ef85e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546075"
---
# <a name="how-to-programmatically-copy-worksheets"></a>Como: copiar planilhas programaticamente
  Você pode criar uma cópia de uma planilha e inserir essa planilha antes ou depois de uma planilha existente na pasta de trabalho. Se você não especificar onde inserir a planilha, o Excel criará uma nova pasta de trabalho para conter a nova planilha.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

> [!NOTE]
> Se você copiar a planilha programaticamente ou o usuário final copiar a planilha manualmente, não haverá nenhum código por trás da nova planilha e os controles na nova planilha não funcionarão. Isso ocorre porque a planilha copiada recentemente é um <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto e não um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host. Controles de Windows Forms e de host só podem ser adicionados a itens de host. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-document-level-customization"></a>Para adicionar uma planilha copiada a uma pasta de trabalho em uma personalização em nível de documento

1. Use o <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> método para copiar a primeira planilha na pasta de trabalho atual e coloque a cópia após a terceira planilha.

     [!code-csharp[Trin_VstcoreExcelAutomation#16](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#16)]
     [!code-vb[Trin_VstcoreExcelAutomation#16](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#16)]

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-vsto-add-in"></a>Para adicionar uma planilha copiada a uma pasta de trabalho em um suplemento do VSTO

1. Use o <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> método para copiar a primeira planilha na pasta de trabalho atual e coloque a cópia após a terceira planilha.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#12](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#12)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#12](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#12)]

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Como: adicionar programaticamente novas planilhas a pastas de trabalho](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [Como: excluir programaticamente planilhas de pastas de trabalho](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [Como: selecionar planilhas programaticamente](../vsto/how-to-programmatically-select-worksheets.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
