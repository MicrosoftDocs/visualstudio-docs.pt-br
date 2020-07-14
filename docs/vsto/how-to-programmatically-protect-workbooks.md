---
title: 'Como: proteger pastas de trabalho programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, passwords
- documents [Office development in Visual Studio], document protection
- workbooks, unprotecting
- document protection, removing from workbooks
- document protection, adding to workbooks
- workbooks, protecting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ee7444c63c2d774e9b22ea612049f09429729c79
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537625"
---
# <a name="how-to-programmatically-protect-workbooks"></a>Como: proteger pastas de trabalho programaticamente
  Você pode proteger um Microsoft Office pasta de trabalho do Excel para que os usuários não possam adicionar ou excluir planilhas e também desproteger a pasta de trabalho programaticamente. Opcionalmente, você pode especificar uma senha, indicar se deseja que a estrutura seja protegida (para que os usuários não possam mover as planilhas) e indicar se deseja que o Windows da pasta de trabalho seja protegido.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 A proteção de uma pasta de trabalho não impede que os usuários editem células. Para proteger os dados, você deve proteger as planilhas. Para obter mais informações, consulte [como: programaticamente proteger planilhas](../vsto/how-to-programmatically-protect-worksheets.md).

 Os exemplos de código a seguir usam uma variável para conter uma senha que é obtida do usuário.

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>Proteger uma pasta de trabalho que faz parte de uma personalização em nível de documento

### <a name="to-protect-a-workbook"></a>Para proteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> método da pasta de trabalho e inclua uma senha. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe, não em uma classe de planilha.

     [!code-csharp[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#10)]
     [!code-vb[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#10)]

### <a name="to-unprotect-a-workbook"></a>Para desproteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> método, passando uma senha, se necessário. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe, não em uma classe de planilha.

     [!code-csharp[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#11)]

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>Proteger uma pasta de trabalho usando um suplemento em nível de aplicativo

### <a name="to-protect-a-workbook"></a>Para proteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A> método da pasta de trabalho e inclua uma senha. Este exemplo de código usa a pasta de trabalho ativa. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#6)]

### <a name="to-unprotect-a-workbook"></a>Para desproteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A> método da pasta de trabalho ativa, passando uma senha, se necessário. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>Confira também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
