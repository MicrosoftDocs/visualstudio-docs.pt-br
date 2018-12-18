---
title: 'Como: programaticamente, agrupar linhas em uma planilha'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: aa9624f90a337fb85ba2868b3b5c4f3cb1553ffb
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258730"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>Como: programaticamente, agrupar linhas em uma planilha
  Você pode agrupar um ou mais linhas inteiras. Para criar um grupo em uma planilha, use um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ou um objeto de intervalo do Excel nativo.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="use-a-namedrange-control"></a>Usar um controle NamedRange  
 Se você adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a um projeto de nível de documento em tempo de design, você pode usar o controle para criar programaticamente um grupo. O exemplo a seguir pressupõe que há três <xref:Microsoft.Office.Tools.Excel.NamedRange> controles na mesma planilha: `data2001`, `data2002`, e `dataAll`. Cada intervalo nomeado se refere a uma linha inteira na planilha.  
  
### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>Para criar um grupo de controles NamedRange em uma planilha  
  
1.  Grupo de três intervalos nomeados, chamando o <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> método de cada intervalo. Esse código deve ser colocado em uma classe de folha, não no `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]  
  
    > [!NOTE]  
    >  Para desagrupar linhas, chame o <xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> método.  
  
## <a name="use-native-excel-ranges"></a>Use o native intervalos do Excel  
 O código pressupõe que você tenha três intervalos do Excel denominados `data2001`, `data2002`, e `dataAll` em uma planilha.  
  
### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>Para criar um grupo de intervalos do Excel em uma planilha  
  
1.  Grupo de três intervalos nomeados, chamando o <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> método de cada intervalo. O exemplo a seguir pressupõe que há três <xref:Microsoft.Office.Interop.Excel.Range> controles denominados `data2001`, `data2002`, e `dataAll` na mesma planilha. Cada intervalo nomeado se refere a uma linha inteira na planilha.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]  
  
    > [!NOTE]  
    >  Para desagrupar linhas, chame o <xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> método.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  