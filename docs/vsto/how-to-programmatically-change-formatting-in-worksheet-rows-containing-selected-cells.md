---
title: 'Como: Alterar programaticamente a formatação em linhas de planilhas que contêm células selecionadas'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio]
- formatting [Office development in Visual Studio]
- worksheets, changing formatting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52b96ce077ed2f45c22679c1be798ae8b2197e0a
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56644985"
---
# <a name="how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells"></a>Como: Alterar programaticamente a formatação em linhas de planilhas que contêm células selecionadas
  Você pode alterar a fonte de uma linha inteira que contém uma célula selecionada para que o texto está em negrito.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-make-the-current-row-bold-and-the-previously-bolded-row-normal"></a>Para tornar a linha atual em negrito e o anteriormente em negrito linha normal

1. Declare uma variável estática para controlar a linha selecionada anteriormente.

    [!code-csharp[Trin_VstcoreExcelAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#37)]
    [!code-vb[Trin_VstcoreExcelAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#37)]

2. Recuperar uma referência para a célula atual usando o <xref:Microsoft.Office.Interop.Excel._Application.ActiveCell%2A> propriedade.

    [!code-csharp[Trin_VstcoreExcelAutomation#38](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#38)]
    [!code-vb[Trin_VstcoreExcelAutomation#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#38)]

3. Estilo atual linha em negrito usando o <xref:Microsoft.Office.Interop.Excel.Range.EntireRow%2A> propriedade da célula ativa.

    [!code-csharp[Trin_VstcoreExcelAutomation#39](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#39)]
    [!code-vb[Trin_VstcoreExcelAutomation#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#39)]

4. Certifique-se de que o valor atual da `previousRow` é não em 0. Um 0 (zero) indica que essa é a primeira vez que esse código.

    [!code-csharp[Trin_VstcoreExcelAutomation#40](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#40)]
    [!code-vb[Trin_VstcoreExcelAutomation#40](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#40)]

5. Certifique-se de que a linha atual é diferente da linha anterior.

    [!code-csharp[Trin_VstcoreExcelAutomation#41](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#41)]
    [!code-vb[Trin_VstcoreExcelAutomation#41](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#41)]

6. Recuperar uma referência a um intervalo que representa a linha que foi selecionada anteriormente e defina essa linha não seja em negrito.

    [!code-csharp[Trin_VstcoreExcelAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#42)]
    [!code-vb[Trin_VstcoreExcelAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#42)]

7. Store a linha atual para que ele pode se tornar a linha anterior na próxima passagem.

    [!code-csharp[Trin_VstcoreExcelAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#43)]
    [!code-vb[Trin_VstcoreExcelAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#43)]

   O exemplo a seguir mostra o método complete.

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_VstcoreExcelAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#36)]
 [!code-vb[Trin_VstcoreExcelAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#36)]

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: Aplicar estilos a intervalos em pastas de trabalho programaticamente](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como: Copiar dados e formatar em planilhas de forma programática](../vsto/how-to-programmatically-copy-data-and-formatting-across-worksheets.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
