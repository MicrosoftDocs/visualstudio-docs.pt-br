---
title: 'Como: aplicar estilos programaticamente a intervalos em pastas de trabalho'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d6f115468bccc2d805b019b9a0ef15cea3605f36
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546153"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>Como: aplicar estilos programaticamente a intervalos em pastas de trabalho
  Você pode aplicar estilos nomeados a regiões em pastas de trabalho. O Excel fornece vários estilos predefinidos.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 A caixa de diálogo **Formatar células** exibe todas as opções que você pode usar para formatar células, e cada uma dessas opções está disponível no seu código. Para exibir essa caixa de diálogo no Excel, clique em **células** no menu **Formatar** .

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>Para aplicar um estilo a um intervalo nomeado em uma personalização no nível do documento

1. Crie um novo estilo e defina seus atributos.

     [!code-csharp[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#53)]
     [!code-vb[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#53)]

2. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle, atribua o texto a ele e aplique o novo estilo. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#54)]
     [!code-vb[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#54)]

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>Para limpar um estilo de um intervalo nomeado em uma personalização no nível do documento

1. Aplique o estilo normal ao intervalo. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     [!code-csharp[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#55)]
     [!code-vb[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#55)]

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>Para aplicar um estilo a um intervalo nomeado em um suplemento do VSTO

1. Crie um novo estilo e defina seus atributos.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#28)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#28)]

2. Crie um <xref:Microsoft.Office.Interop.Excel.Range> , atribua um texto a ele e, em seguida, aplique o novo estilo.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#29)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#29)]

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>Para limpar um estilo de um intervalo nomeado em um suplemento do VSTO

1. Aplique o estilo normal ao intervalo.

     [!code-csharp[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#56)]
     [!code-vb[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#56)]

## <a name="see-also"></a>Consulte também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
