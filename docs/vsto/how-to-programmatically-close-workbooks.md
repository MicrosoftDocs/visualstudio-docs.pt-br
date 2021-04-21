---
title: 'Como: fechar pastas de trabalho programaticamente'
description: Saiba como você pode fechar a pasta de trabalho ativa ou pode especificar uma pasta de trabalho para fechar programaticamente.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d09cbff06b1bb7048316629b7b958ee299029ec8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825258"
---
# <a name="how-to-programmatically-close-workbooks"></a>Como: fechar pastas de trabalho programaticamente
  Você pode fechar a pasta de trabalho ativa ou pode especificar uma pasta de trabalho para fechar.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="close-the-active-workbook"></a>Fechar a pasta de trabalho ativa
 Há dois procedimentos para fechar a pasta de trabalho ativa: uma para personalizações em nível de documento e outra para os suplementos do VSTO.

### <a name="to-close-the-active-workbook-in-a-document-level-customization"></a>Para fechar a pasta de trabalho ativa em uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Close%2A> método para fechar a pasta de trabalho associada à personalização. Para usar o exemplo de código a seguir, execute-o na `Sheet1` classe em um projeto de nível de documento para Excel.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet3":::

### <a name="to-close-the-active-workbook-in-a-vsto-add-in"></a>Para fechar a pasta de trabalho ativa em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Close%2A> método para fechar a pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet1":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet1":::

## <a name="close-a-workbook-that-you-specify-by-name"></a>Fechar uma pasta de trabalho que você especificar por nome
 A maneira de fechar uma pasta de trabalho que você especifica por nome é a mesma para suplementos do VSTO e personalizações em nível de documento.

### <a name="to-close-a-workbook-that-you-specify-by-name"></a>Para fechar uma pasta de trabalho que você especificar por nome

1. Especifique o nome da pasta de trabalho como um argumento para a <xref:Microsoft.Office.Interop.Excel.Workbooks> coleção. O exemplo de código a seguir pressupõe que uma pasta de trabalho chamada **NewWorkbook** está aberta no Excel.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet2":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Como: salvar pastas de trabalho programaticamente](../vsto/how-to-programmatically-save-workbooks.md)
- [Como: pastas de trabalho abertas programaticamente](../vsto/how-to-programmatically-open-workbooks.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
