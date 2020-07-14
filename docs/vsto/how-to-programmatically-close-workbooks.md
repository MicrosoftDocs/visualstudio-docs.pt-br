---
title: 'Como: fechar pastas de trabalho programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, closing
- Excel [Office development in Visual Studio], closing workbooks
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3d3fe0f929632bd7021def9f6597182aa8fea87b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547492"
---
# <a name="how-to-programmatically-close-workbooks"></a>Como: fechar pastas de trabalho programaticamente
  Você pode fechar a pasta de trabalho ativa ou pode especificar uma pasta de trabalho para fechar.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="close-the-active-workbook"></a>Fechar a pasta de trabalho ativa
 Há dois procedimentos para fechar a pasta de trabalho ativa: uma para personalizações em nível de documento e outra para os suplementos do VSTO.

### <a name="to-close-the-active-workbook-in-a-document-level-customization"></a>Para fechar a pasta de trabalho ativa em uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Close%2A> método para fechar a pasta de trabalho associada à personalização. Para usar o exemplo de código a seguir, execute-o na `Sheet1` classe em um projeto de nível de documento para Excel.

     [!code-csharp[Trin_VstcoreExcelAutomation#3](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#3)]
     [!code-vb[Trin_VstcoreExcelAutomation#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#3)]

### <a name="to-close-the-active-workbook-in-a-vsto-add-in"></a>Para fechar a pasta de trabalho ativa em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Close%2A> método para fechar a pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#1](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#1)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#1](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#1)]

## <a name="close-a-workbook-that-you-specify-by-name"></a>Fechar uma pasta de trabalho que você especificar por nome
 A maneira de fechar uma pasta de trabalho que você especifica por nome é a mesma para suplementos do VSTO e personalizações em nível de documento.

### <a name="to-close-a-workbook-that-you-specify-by-name"></a>Para fechar uma pasta de trabalho que você especificar por nome

1. Especifique o nome da pasta de trabalho como um argumento para a <xref:Microsoft.Office.Interop.Excel.Workbooks> coleção. O exemplo de código a seguir pressupõe que uma pasta de trabalho chamada **NewWorkbook** está aberta no Excel.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#2](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#2)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#2](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#2)]

## <a name="see-also"></a>Confira também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Como: salvar pastas de trabalho programaticamente](../vsto/how-to-programmatically-save-workbooks.md)
- [Como: pastas de trabalho abertas programaticamente](../vsto/how-to-programmatically-open-workbooks.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
