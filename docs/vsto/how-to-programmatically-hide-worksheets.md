---
title: 'Como: ocultar planilhas programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 83cf1f63a67525dca4cf9dbb5a4916da5d70b4ce
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547401"
---
# <a name="how-to-programmatically-hide-worksheets"></a>Como: ocultar planilhas programaticamente
  Você pode mostrar ou ocultar qualquer planilha em uma pasta de trabalho. Para ocultar uma planilha, use o item de host da planilha ou acesse a planilha usando a coleção planilhas da pasta de trabalho.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>Usar o item de host da planilha
 Se a planilha foi adicionada em tempo de design em uma personalização em nível de documento, use a <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> propriedade para ocultar a planilha especificada.

### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>Para ocultar uma planilha usando um item de host de planilha

1. Defina a <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> Propriedade do `Sheet1` item de host para o <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> valor de enumeração.

     [!code-csharp[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#25)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção Sheets da pasta de trabalho do Excel
 Acesse planilhas por meio da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção Microsoft Office Excel nos seguintes casos:

- Você deseja ocultar uma planilha em um suplemento do VSTO.

- A planilha que você deseja ocultar foi criada em tempo de execução em uma personalização no nível do documento.

### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>Para ocultar uma planilha usando a coleção Sheets da pasta de trabalho do Excel

1. Defina a <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> propriedade da planilha para o <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> valor de enumeração.

     [!code-csharp[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#26)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: excluir programaticamente planilhas de pastas de trabalho](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [Como: mover planilhas programaticamente dentro de pastas de trabalho](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
