---
title: 'Como: aplicar de forma programática cores a intervalos do Excel'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- color, Excel ranges
- ranges, applying color
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0d4a99e2e71e6a87b304ceea45a3cd595f911ff1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543449"
---
# <a name="how-to-programmatically-apply-color-to-excel-ranges"></a>Como: aplicar de forma programática cores a intervalos do Excel
  Para aplicar uma cor ao texto em um intervalo de células, use um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou um objeto Range do Excel nativo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange
 Este exemplo é para personalizações em nível de documento.

### <a name="to-apply-color-to-a-namedrange-control"></a>Para aplicar cor a um controle NamedRange

1. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na célula a1.

     [!code-csharp[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#65)]
     [!code-vb[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#65)]

2. Defina a cor do texto no <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.

     [!code-csharp[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#66)]
     [!code-vb[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#66)]

## <a name="use-native-excel-ranges"></a>Usar intervalos nativos do Excel

### <a name="to-apply-color-to-a-native-excel-range-object"></a>Para aplicar cor a um objeto de intervalo do Excel nativo

1. Crie um intervalo na célula a1 e defina a cor do texto.

     [!code-csharp[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#67)]
     [!code-vb[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#67)]

## <a name="see-also"></a>Confira também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
