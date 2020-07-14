---
title: Preenchimento incremental de intervalos de dados de forma dinâmica
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Autofill method [Excel]
- filling ranges automatically
- ranges, automatically filling
- workbooks, filling ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 076381c93d11c2d13bdd89ea5c36c0039e15ef71
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547466"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>Como: preencher intervalos de forma programática automaticamente com dados em alteração incremental
  O <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método do <xref:Microsoft.Office.Interop.Excel.Range> objeto permite preencher um intervalo em uma planilha com valores automaticamente. Geralmente, o <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método é usado para armazenar valores incrementalmente crescentes ou decrescentes em um intervalo. Você pode especificar o comportamento fornecendo uma constante opcional da <xref:Microsoft.Office.Interop.Excel.XlAutoFillType> enumeração.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Você deve especificar dois intervalos ao usar <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> :

- O intervalo que chama o <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método, que especifica o ponto inicial do preenchimento e contém um valor inicial.

- O intervalo que você deseja preencher, passado como um parâmetro para o <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método. Esse intervalo de destino deve incluir o intervalo que contém o valor inicial.

    > [!NOTE]
    > Não é possível passar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle no lugar do <xref:Microsoft.Office.Interop.Excel.Range> . Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#49)]
 [!code-vb[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#49)]

## <a name="compile-the-code"></a>Compilar o código
 A primeira célula do intervalo que você deseja preencher deve conter um valor inicial.

 O exemplo requer que você preencha três regiões:

- A coluna B é incluir cinco dias da semana. Para o valor inicial, digite **segunda-feira** na célula B1.

- A coluna C é incluir cinco meses. Para o valor inicial, digite **janeiro** na célula C1.

- A coluna D é incluir uma série de números, incrementando por dois para cada linha. Para os valores iniciais, digite **4** na célula D1 e **6** na célula D2.

## <a name="see-also"></a>Confira também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como executar cálculos do Excel programaticamente](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
