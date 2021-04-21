---
title: 'Como: salvar pastas de trabalho programaticamente'
description: Salve programaticamente pastas de trabalho do Microsoft Excel sem alterar o caminho e salve uma cópia de uma pasta de trabalho sem modificar a pasta de trabalho aberta na memória.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, saving in XML format
- workbooks, saving
- workbooks, saving backup copies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4559d098a80a1dfd8f1d3f5c2c21cbebc992fcb7
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828976"
---
# <a name="how-to-programmatically-save-workbooks"></a>Como: salvar pastas de trabalho programaticamente
  Há várias maneiras de salvar uma pasta de trabalho. Você pode salvar uma pasta de trabalho sem alterar o caminho. Se a pasta de trabalho não tiver sido salva antes, você deverá salvar a pasta de trabalho especificando um caminho. Sem um caminho explícito, Microsoft Office Excel salva o arquivo na pasta atual com o nome que foi fornecido quando foi criado. Você também pode salvar uma cópia da pasta de trabalho sem modificar a pasta de trabalho aberta na memória.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="save-a-workbook-without-changing-the-path"></a>Salvar uma pasta de trabalho sem alterar o caminho

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Save%2A> método da `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet4":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.Save%2A> método para salvar a pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet3":::

## <a name="save-a-workbook-with-a-new-path"></a>Salvar uma pasta de trabalho com um novo caminho
 Você pode salvar a pasta de trabalho especificada em um novo local ou com um novo nome, opcionalmente especificando um formato de arquivo, uma senha, um modo de acesso e muito mais.

> [!NOTE]
> Talvez você queira definir a <xref:Microsoft.Office.Interop.Excel._Application.DisplayAlerts%2A> propriedade como **false** antes de salvar a pasta de trabalho com um novo caminho, pois salvar em alguns formatos requer interação. Definir essa propriedade como **false** faz com que o Excel use todos os padrões.

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> método da `ThisWorkbook` classe. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet5":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.SaveAs%2A> método para salvar a pasta de trabalho ativa em um novo caminho. Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet4":::

## <a name="save-a-copy-of-the-workbook"></a>Salvar uma cópia da pasta de trabalho
 Você pode salvar uma cópia da pasta de trabalho em um arquivo sem modificar a pasta de trabalho aberta na memória. Isso é útil quando você deseja criar uma cópia de backup sem modificar o local da pasta de trabalho.

### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveCopyAs%2A> método da `ThisWorkbook` classe. Para usar o exemplo de código a seguir, execute-o na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet6":::

### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Workbook.SaveCopyAs%2A> método para salvar uma cópia da pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet5":::

## <a name="robust-programming"></a>Programação robusta
 O cancelamento interativo de qualquer um dos métodos que salvam ou copiam a pasta de trabalho gera um erro em tempo de execução em seu código. Por exemplo, se o procedimento chama o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> método, mas não desabilita prompts do Excel e o usuário clica em **Cancelar** quando solicitado, o Excel gera um erro em tempo de execução.

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Item de host da pasta de trabalho](../vsto/workbook-host-item.md)
- [Como: fechar pastas de trabalho programaticamente](../vsto/how-to-programmatically-close-workbooks.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
