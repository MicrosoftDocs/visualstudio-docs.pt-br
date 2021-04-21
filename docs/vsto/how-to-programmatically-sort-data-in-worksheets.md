---
title: 'Como: classificar dados de forma programática em planilhas'
description: Saiba como você pode usar o Visual Studio para classificar programaticamente dados contidos em intervalos de planilha e listas em tempo de execução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data sorting, worksheets
- data [Office development in Visual Studio], sorting in worksheets
- worksheets, sorting data
- sorting data, in worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 024bf53b7fc7f3a6e32e10b7107c9a62d8c40cee
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825011"
---
# <a name="how-to-programmatically-sort-data-in-worksheets"></a>Como: classificar dados de forma programática em planilhas
  Você pode classificar os dados contidos em intervalos de planilha e listas em tempo de execução. O código a seguir classifica um intervalo de várias colunas nomeado `Fruits` pelos dados na primeira coluna e, em seguida, pelos dados na segunda coluna.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="sort-data-in-a-document-level-customization"></a>Classificar dados em uma personalização no nível do documento

### <a name="to-sort-data-in-a-namedrange-control"></a>Para classificar dados em um controle NamedRange

1. Chame o <xref:Microsoft.Office.Tools.Excel.NamedRange.Sort%2A> método do <xref:Microsoft.Office.Tools.Excel.NamedRange> controle. O exemplo a seguir requer um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `Fruits` em uma planilha. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet78":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet78":::

   Coloque o código a seguir em *Plan1. vb* ou *Plan1. cs* para classificar dados em um <xref:Microsoft.Office.Tools.Excel.ListObject> controle. O código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `fruitList` em uma planilha chamada `Sheet1` .

### <a name="to-sort-data-in-a-listobject-control"></a>Para classificar dados em um controle ListObject

1. Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método da <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> Propriedade do controle de <xref:Microsoft.Office.Tools.Excel.ListObject> host.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet79":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet79":::

## <a name="sort-data-in-a-vsto-add-in"></a>Classificar dados em um suplemento do VSTO

### <a name="to-sort-data-in-a-native-range"></a>Para classificar dados em um intervalo nativo

1. Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método do controle nativo do Excel <xref:Microsoft.Office.Interop.Excel.Range> . O exemplo a seguir requer um controle nativo do Excel chamado `Fruits` em uma planilha.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet23":::

### <a name="to-sort-data-in-a-listobject-control"></a>Para classificar dados em um controle ListObject

1. Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método da <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> Propriedade do controle nativo do Excel <xref:Microsoft.Office.Interop.Excel.ListObject> . O exemplo a seguir pressupõe que você tenha um controle nativo do Excel <xref:Microsoft.Office.Interop.Excel.ListObject> chamado `fruitList` na planilha ativa.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet24":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: preencher intervalos de forma programática automaticamente com dados em alteração incremental](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
