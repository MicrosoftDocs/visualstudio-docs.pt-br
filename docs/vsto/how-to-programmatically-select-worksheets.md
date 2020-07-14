---
title: 'Como: selecionar planilhas programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, selecting
- Excel projects, selecting worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6134b23e7b398794529ee43a428ee8b8962ccf38
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546998"
---
# <a name="how-to-programmatically-select-worksheets"></a>Como: selecionar planilhas programaticamente
  O <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> método seleciona o objeto especificado, que move a seleção do usuário para o novo objeto. Use o <xref:Microsoft.Office.Tools.Excel.Worksheet.Activate%2A> método se desejar colocar o foco no objeto sem alterar a seleção do usuário.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Se você quiser selecionar uma planilha existente em um suplemento do VSTO ou se a planilha tiver sido criada em tempo de execução em uma personalização em nível de documento, você deverá acessá-la usando a <xref:Microsoft.Office.Interop.Excel.Sheets> coleção do Excel da pasta de trabalho do Excel; caso contrário, você poderá acessar o <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host diretamente.

## <a name="use-the-worksheet-host-item"></a>Usar o item de host da planilha
 Em uma personalização no nível do documento, adicione o código a seguir a *Plan1. vb* ou *Sheet1.cs*.

### <a name="to-select-the-first-worksheet-in-a-workbook-using-a-host-item"></a>Para selecionar a primeira planilha em uma pasta de trabalho usando um item de host

1. Chame o método <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> de `Sheet1`.

     [!code-csharp[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#19)]
     [!code-vb[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#19)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção Sheets da pasta de trabalho do Excel
 Acesse a planilha usando a coleção do Excel <xref:Microsoft.Office.Interop.Excel.Sheets> .

### <a name="to-select-the-first-worksheet-in-a-workbook-using-the-sheets-collection-of-the-excel-workbook"></a>Para selecionar a primeira planilha em uma pasta de trabalho usando a coleção Sheets da pasta de trabalho do Excel

1. Chame o <xref:Microsoft.Office.Interop.Excel.Sheets.Select%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção para selecionar a primeira planilha da pasta de trabalho ativa.

     [!code-csharp[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#20)]
     [!code-vb[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#20)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: imprimir planilhas programaticamente](../vsto/how-to-programmatically-print-worksheets.md)
- [Como: excluir programaticamente planilhas de pastas de trabalho](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Item de host de planilha](../vsto/worksheet-host-item.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
