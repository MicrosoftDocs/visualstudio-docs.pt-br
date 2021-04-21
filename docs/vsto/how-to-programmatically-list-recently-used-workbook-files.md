---
title: Como programaticamente listar arquivos de pasta de trabalho usados recentemente
description: Saiba como você pode listar programaticamente os arquivos de pasta de trabalho do Microsoft Excel usados recentemente usando o Visual Studio.
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ba7ca717af4330e8fb3c102b3a5fe5bf7d9162b6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825323"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>Como programaticamente listar arquivos de pasta de trabalho usados recentemente
  A <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A> propriedade retorna uma coleção que contém os nomes de todos os arquivos que aparecem na lista Microsoft Office Excel de arquivos usados recentemente. O comprimento da lista varia dependendo do número de arquivos que o usuário selecionou para reter. Você pode exibir os resultados em um intervalo.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>Para listar pastas de trabalho usadas recentemente em um objeto de intervalo

1. Execute um loop na lista de arquivos recentes e exiba os nomes em células relativas a um <xref:Microsoft.Office.Interop.Excel.Range> objeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet9":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
