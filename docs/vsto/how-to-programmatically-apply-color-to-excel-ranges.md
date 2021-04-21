---
title: 'Como: aplicar de forma programática cores a intervalos do Excel'
description: Saiba que, para aplicar uma cor ao texto em um intervalo de células, você usa um controle NamedRange ou um objeto Range do Excel nativo.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 081985dbd4b235fe5dd8d3472d0ab574603abe1b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828313"
---
# <a name="how-to-programmatically-apply-color-to-excel-ranges"></a>Como: aplicar de forma programática cores a intervalos do Excel
  Para aplicar uma cor ao texto em um intervalo de células, use um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou um objeto Range do Excel nativo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange
 Este exemplo é para personalizações em nível de documento.

### <a name="to-apply-color-to-a-namedrange-control"></a>Para aplicar cor a um controle NamedRange

1. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na célula a1.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet65":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet65":::

2. Defina a cor do texto no <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet66":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet66":::

## <a name="use-native-excel-ranges"></a>Usar intervalos nativos do Excel

### <a name="to-apply-color-to-a-native-excel-range-object"></a>Para aplicar cor a um objeto de intervalo do Excel nativo

1. Crie um intervalo na célula a1 e defina a cor do texto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet67":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet67":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
