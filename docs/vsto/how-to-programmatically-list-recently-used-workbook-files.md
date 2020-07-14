---
title: Como programaticamente listar arquivos de pasta de trabalho usados recentemente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing recently used
- RecentFiles property
- Excel [Office development in Visual Studio], recently used files listing
- recent file list, Excel
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4f4f34a8ed848d548b2e23d3f9a3cf3c603c7cad
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541356"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>Como programaticamente listar arquivos de pasta de trabalho usados recentemente
  A <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A> propriedade retorna uma coleção que contém os nomes de todos os arquivos que aparecem na lista Microsoft Office Excel de arquivos usados recentemente. O comprimento da lista varia dependendo do número de arquivos que o usuário selecionou para reter. Você pode exibir os resultados em um intervalo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>Para listar pastas de trabalho usadas recentemente em um objeto de intervalo

1. Execute um loop na lista de arquivos recentes e exiba os nomes em células relativas a um <xref:Microsoft.Office.Interop.Excel.Range> objeto.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#9)]

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
