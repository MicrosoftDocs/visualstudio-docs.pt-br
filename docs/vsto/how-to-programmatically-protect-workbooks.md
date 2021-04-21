---
title: 'Como: proteger pastas de trabalho programaticamente'
description: Saiba como você pode proteger uma pasta de trabalho do Microsoft Excel para que os usuários não possam adicionar ou excluir planilhas e também desproteger a pasta de trabalho programaticamente.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9f0b479c56be6da7b14f87263c8c01d66910ac20
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827099"
---
# <a name="how-to-programmatically-protect-workbooks"></a>Como: proteger pastas de trabalho programaticamente
  Você pode proteger um Microsoft Office pasta de trabalho do Excel para que os usuários não possam adicionar ou excluir planilhas e também desproteger a pasta de trabalho programaticamente. Opcionalmente, você pode especificar uma senha, indicar se deseja que a estrutura seja protegida (para que os usuários não possam mover as planilhas) e indicar se deseja que o Windows da pasta de trabalho seja protegido.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 A proteção de uma pasta de trabalho não impede que os usuários editem células. Para proteger os dados, você deve proteger as planilhas. Para obter mais informações, consulte [como: programaticamente proteger planilhas](../vsto/how-to-programmatically-protect-worksheets.md).

 Os exemplos de código a seguir usam uma variável para conter uma senha que é obtida do usuário.

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>Proteger uma pasta de trabalho que faz parte de uma personalização em nível de documento

### <a name="to-protect-a-workbook"></a>Para proteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> método da pasta de trabalho e inclua uma senha. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe, não em uma classe de planilha.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet10":::

### <a name="to-unprotect-a-workbook"></a>Para desproteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> método, passando uma senha, se necessário. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe, não em uma classe de planilha.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet11":::

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>Proteger uma pasta de trabalho usando um suplemento em nível de aplicativo

### <a name="to-protect-a-workbook"></a>Para proteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A> método da pasta de trabalho e inclua uma senha. Este exemplo de código usa a pasta de trabalho ativa. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet6":::

### <a name="to-unprotect-a-workbook"></a>Para desproteger uma pasta de trabalho

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A> método da pasta de trabalho ativa, passando uma senha, se necessário. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
