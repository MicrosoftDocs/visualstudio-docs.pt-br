---
title: 'Como: classificar dados em planilhas de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data sorting, worksheets
- data [Office development in Visual Studio], sorting in worksheets
- worksheets, sorting data
- sorting data, in worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 179cf5fab5a1b2690cb4b46160f7a5c3342fe7bc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914200"
---
# <a name="how-to-programmatically-sort-data-in-worksheets"></a>Como: classificar dados em planilhas de forma programática
  Você pode classificar os dados contidos nas listas e intervalos de planilhas em tempo de execução. O código a seguir classifica um intervalo de várias coluna chamado `Fruits` os dados na primeira coluna e, em seguida, pelos dados na segunda coluna.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="sort-data-in-a-document-level-customization"></a>Classificar dados em uma personalização no nível de documento  
  
### <a name="to-sort-data-in-a-namedrange-control"></a>Para classificar dados em um controle NamedRange  
  
1. Chame o <xref:Microsoft.Office.Tools.Excel.NamedRange.Sort%2A> método da <xref:Microsoft.Office.Tools.Excel.NamedRange> controle. O exemplo a seguir exige um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `Fruits` em uma planilha. Esse código deve ser colocado em uma classe de folha, não no `ThisWorkbook` classe.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#78)]
    [!code-vb[Trin_VstcoreExcelAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#78)]  
  
   Coloque o seguinte código no *Sheet1.vb* ou *Sheet1.cs* para classificar dados em um <xref:Microsoft.Office.Tools.Excel.ListObject> controle. O código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `fruitList` em uma planilha denominada `Sheet1`.  
  
### <a name="to-sort-data-in-a-listobject-control"></a>Para classificar dados em um controle ListObject  
  
1.  Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método da <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> propriedade do <xref:Microsoft.Office.Tools.Excel.ListObject> controle de host.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#79)]
     [!code-vb[Trin_VstcoreExcelAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#79)]  
  
## <a name="sort-data-in-a-vsto-add-in"></a>Classificar dados em um suplemento do VSTO  
  
### <a name="to-sort-data-in-a-native-range"></a>Para classificar dados em um intervalo nativo  
  
1.  Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método do Excel nativo <xref:Microsoft.Office.Interop.Excel.Range> controle. O exemplo a seguir exige um controle nativo do Excel chamado `Fruits` em uma planilha.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#23](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#23](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#23)]  
  
### <a name="to-sort-data-in-a-listobject-control"></a>Para classificar dados em um controle ListObject  
  
1.  Chame o <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> método da <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> propriedade do Excel nativo <xref:Microsoft.Office.Interop.Excel.ListObject> controle. O exemplo a seguir pressupõe que você tenha um arquivo do Excel nativo <xref:Microsoft.Office.Interop.Excel.ListObject> controle chamado `fruitList` na planilha ativa.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#24](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#24)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#24](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#24)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: preencher automaticamente por meio de programação intervalos com dados alterados em incrementos](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)   
 [Como: por meio de programação se referir a intervalos de planilhas em código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)   
 [Como: aplicar estilos a intervalos em pastas de trabalho programaticamente](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Controle ListObject](../vsto/listobject-control.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  