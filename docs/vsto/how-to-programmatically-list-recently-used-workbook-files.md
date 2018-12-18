---
title: 'Como: programaticamente listar arquivos usados recentemente pasta de trabalho'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing recently used
- RecentFiles property
- Excel [Office development in Visual Studio], recently used files listing
- recent file list, Excel
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d3e909ad3e1509689d953e0ad6c6b8346ff97f91
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257583"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>Como: programaticamente listar arquivos usados recentemente pasta de trabalho
  O <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A> propriedade retorna uma coleção que contém os nomes de todos os arquivos que aparecem na lista de arquivos usados recentemente o Microsoft Office Excel. O comprimento da lista varia dependendo do número de arquivos que o usuário tiver selecionado para manter. Você pode exibir os resultados em um intervalo.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>Para pastas de trabalho de lista usada recentemente em um objeto de intervalo  
  
1.  Percorra a lista de arquivos recentes e exibir os nomes nas células relativo a um <xref:Microsoft.Office.Interop.Excel.Range> objeto.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#9)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  