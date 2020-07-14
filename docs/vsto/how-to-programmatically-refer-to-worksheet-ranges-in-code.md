---
title: Como fazer referência programaticamente a intervalos de planilha no código
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, referring to
- worksheets, referring to ranges
- referring to worksheet ranges
- Excel [Office development in Visual Studio], referring to worksheet ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 93673fcc270ce2f1ac43804cb1d794281f28c702
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547388"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>Como fazer referência programaticamente a intervalos de planilha no código
  Você usa um processo semelhante para fazer referência ao conteúdo de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou a um objeto Range do Excel nativo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange
 O exemplo a seguir adiciona um <xref:Microsoft.Office.Tools.Excel.NamedRange> a uma planilha e, em seguida, adiciona o texto à célula no intervalo.

### <a name="to-refer-to-a-namedrange-control"></a>Para fazer referência a um controle NamedRange

1. Atribua uma cadeia de caracteres à <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> Propriedade do <xref:Microsoft.Office.Tools.Excel.NamedRange> controle. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#46)]
     [!code-vb[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#46)]

## <a name="use-native-excel-ranges"></a>Usar intervalos nativos do Excel
 O exemplo a seguir adiciona um intervalo do Excel nativo a uma planilha e, em seguida, adiciona o texto à célula no intervalo.

### <a name="to-refer-to-a-native-range-object"></a>Para fazer referência a um objeto de intervalo nativo

1. Atribua uma cadeia de caracteres à <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> Propriedade do intervalo.

     [!code-csharp[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#47)]
     [!code-vb[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#47)]

## <a name="see-also"></a>Confira também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Como: verificar a ortografia em planilhas programaticamente](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como: preencher intervalos de forma programática automaticamente com dados em alteração incremental](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [Como: Pesquisar por programação de texto em intervalos de planilhas](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
