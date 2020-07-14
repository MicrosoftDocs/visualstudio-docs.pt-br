---
title: Armazenar & recuperar valores de data em intervalos do Excel programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], retrieving date values from ranges
- ranges, retrieving data values
- dates, retrieving from Excel ranges
- Excel [Office development in Visual Studio], storing date values in ranges
- date values, storing in Excel ranges
- dates, storing in Excel ranges
- ranges, storing date values
- date values
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e4cea02af59b6b6a8457d964bdce802e1e2b2b84
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546959"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>Como armazenar de forma programática e recuperar valores de data em intervalos do Excel
  Você pode armazenar e recuperar valores em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou em um objeto Range do Excel nativo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Se você armazenar um valor de data que se enquadra ou depois de 1/1/1900 em um intervalo usando as ferramentas de desenvolvimento do Office no Visual Studio, ele será armazenado no formato de automação OLE (OA). Você deve usar o <xref:System.DateTime.FromOADate%2A> método para recuperar o valor de datas de automação OLE (OA). Se a data for anterior a 1/1/1900, ela será armazenada como uma cadeia de caracteres.

> [!NOTE]
> As datas do Excel diferem das datas de automação OLE dos primeiros dois meses de 1900. Também há diferenças se a opção de **sistema de data 1904** estiver marcada. Os exemplos de código abaixo não abordam essas diferenças.

## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange

- Este exemplo é para personalizações em nível de documento. O código a seguir deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

### <a name="to-store-a-date-value-in-a-named-range"></a>Para armazenar um valor de data em um intervalo nomeado

1. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na célula **a1**.

     [!code-csharp[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#50)]
     [!code-vb[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#50)]

2. Defina a data de hoje como o valor de `NamedRange1` .

     [!code-csharp[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#51)]
     [!code-vb[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#51)]

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>Para recuperar um valor de data de um intervalo nomeado

1. Recupere o valor de data de `NamedRange1` .

     [!code-csharp[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#52)]
     [!code-vb[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#52)]

## <a name="use-native-excel-ranges"></a>Usar intervalos nativos do Excel

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>Para armazenar um valor de data em um objeto de intervalo do Excel nativo

1. Crie um <xref:Microsoft.Office.Interop.Excel.Range> que representa a célula **a1**.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#25)]

2. Defina a data de hoje como o valor de `rng` .

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#26)]

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>Para recuperar um valor de data de um objeto de intervalo do Excel nativo

1. Recupere o valor de data de `rng` .

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#27)]

## <a name="see-also"></a>Confira também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
