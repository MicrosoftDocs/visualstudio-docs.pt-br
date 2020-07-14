---
title: Copiar dados e formatação entre planilhas programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 07baa23b6fd276e8fb8452934dc6361544d16038
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546101"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>Como: copiar dados e formatação programaticamente em planilhas
  Você pode copiar dados de um intervalo em uma planilha para todas as outras planilhas em uma pasta de trabalho usando o <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> método. Especifique um intervalo e se deseja copiar dados, formatação ou ambos.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#44)]
 [!code-vb[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#44)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer um intervalo chamado `rangeData` em uma planilha.

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: adicionar programaticamente novas planilhas a pastas de trabalho](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [Como: alterar a formatação de forma programática em linhas de planilha contendo células selecionadas](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
