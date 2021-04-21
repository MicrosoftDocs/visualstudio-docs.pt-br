---
title: 'Como: aplicar estilos programaticamente a intervalos em pastas de trabalho'
description: Saiba como você pode aplicar estilos nomeados a regiões em pastas de trabalho. O Excel fornece vários estilos predefinidos.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b1ce30c9a0e21bd4b8860f7a4d17191c48cd2ad9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828300"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>Como: aplicar estilos programaticamente a intervalos em pastas de trabalho
  Você pode aplicar estilos nomeados a regiões em pastas de trabalho. O Excel fornece vários estilos predefinidos.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 A caixa de diálogo **Formatar células** exibe todas as opções que você pode usar para formatar células, e cada uma dessas opções está disponível no seu código. Para exibir essa caixa de diálogo no Excel, clique em **células** no menu **Formatar** .

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>Para aplicar um estilo a um intervalo nomeado em uma personalização no nível do documento

1. Crie um novo estilo e defina seus atributos.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet53":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet53":::

2. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle, atribua o texto a ele e aplique o novo estilo. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet54":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet54":::

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>Para limpar um estilo de um intervalo nomeado em uma personalização no nível do documento

1. Aplique o estilo normal ao intervalo. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet55":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet55":::

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>Para aplicar um estilo a um intervalo nomeado em um suplemento do VSTO

1. Crie um novo estilo e defina seus atributos.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet28":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet28":::

2. Crie um <xref:Microsoft.Office.Interop.Excel.Range> , atribua um texto a ele e, em seguida, aplique o novo estilo.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet29":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet29":::

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>Para limpar um estilo de um intervalo nomeado em um suplemento do VSTO

1. Aplique o estilo normal ao intervalo.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet56":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet56":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
