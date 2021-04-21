---
title: 'Como: programaticamente listar todas as planilhas em uma pasta de trabalho'
description: Saiba como você pode listar todas as planilhas de forma programática em uma pasta de trabalho do Microsoft Excel usando o Visual Studio.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing worksheets
- worksheets, listing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c0cdd57c801617d8b3c37df28b91faae378bc4cc
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824894"
---
# <a name="how-to-programmatically-list-all-worksheets-in-a-workbook"></a>Como: programaticamente listar todas as planilhas em uma pasta de trabalho
  A <xref:Microsoft.Office.Interop.Excel.Workbook> classe fornece um <xref:Microsoft.Office.Interop.Excel.Worksheets> objeto. Este objeto contém uma coleção de todos os <xref:Microsoft.Office.Interop.Excel.Worksheet> objetos na pasta de trabalho.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-document-level-customization"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em uma personalização em nível de documento

1. Iterar pela <xref:Microsoft.Office.Interop.Excel.Worksheets> coleção e enviar o nome de cada planilha para um deslocamento de célula de <xref:Microsoft.Office.Tools.Excel.NamedRange> um controle.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet21":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet21":::

## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-vsto-add-in"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em um suplemento do VSTO

1. Iterar pela <xref:Microsoft.Office.Interop.Excel.Worksheets> coleção e enviar o nome de cada planilha para um deslocamento de célula de <xref:Microsoft.Office.Interop.Excel.Range> um objeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet13":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: adicionar programaticamente novas planilhas a pastas de trabalho](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [Como: mover planilhas programaticamente dentro de pastas de trabalho](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
