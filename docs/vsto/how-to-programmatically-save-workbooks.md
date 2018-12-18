---
title: 'Como: salvar pastas de trabalho de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, saving in XML format
- workbooks, saving
- workbooks, saving backup copies
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6fc715518f31031c65667a2480d7e14111105202
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670062"
---
# <a name="how-to-programmatically-save-workbooks"></a>Como: salvar pastas de trabalho de forma programática
  Há várias maneiras de salvar uma pasta de trabalho. Você pode salvar uma pasta de trabalho sem alterar o caminho. Se a pasta de trabalho não tiver sido salvo antes, você deve salvar a pasta de trabalho, especificando um caminho. Sem um caminho explícito, o Microsoft Office Excel salva o arquivo na pasta atual com o nome que foi fornecido quando ele foi criado. Você também pode salvar uma cópia da pasta de trabalho sem modificar a pasta de trabalho aberta na memória.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="save-a-workbook-without-changing-the-path"></a>Salvar uma pasta de trabalho sem alterar o caminho  
  
### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.Save%2A> método da `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#4](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#4)]
     [!code-vb[Trin_VstcoreExcelAutomation#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#4)]  
  
### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Workbook.Save%2A> método para salvar a pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#3](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#3)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#3](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#3)]  
  
## <a name="save-a-workbook-with-a-new-path"></a>Salvar uma pasta de trabalho com um novo caminho  
 Você pode salvar a pasta de trabalho especificada para um novo local ou com um novo nome, opcionalmente especificando um formato de arquivo, uma senha, um modo de acesso e muito mais.  
  
> [!NOTE]  
>  Você talvez queira definir o <xref:Microsoft.Office.Interop.Excel._Application.DisplayAlerts%2A> propriedade para **falso** antes de salvar a pasta de trabalho com um novo caminho, como salvando em alguns formatos requer interação. Definir essa propriedade como **falsos** faz com que o Excel para usar todos os padrões.  
  
### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> método da `ThisWorkbook` classe. Para usar o exemplo de código a seguir, execute-o `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#5)]
     [!code-vb[Trin_VstcoreExcelAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#5)]  
  
### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Workbook.SaveAs%2A> método para salvar a pasta de trabalho ativa para um novo caminho. Para usar o exemplo de código a seguir, execute-o `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#4](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#4)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#4](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#4)]  
  
## <a name="save-a-copy-of-the-workbook"></a>Salvar uma cópia da pasta de trabalho  
 Você pode salvar uma cópia da pasta de trabalho em um arquivo sem modificar a pasta de trabalho aberta na memória. Isso é útil quando você deseja criar uma cópia de backup sem modificar o local da pasta de trabalho.  
  
### <a name="to-save-a-workbook-associated-with-a-document-level-customization"></a>Para salvar uma pasta de trabalho associada a uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveCopyAs%2A> método da `ThisWorkbook` classe. Para usar o exemplo de código a seguir, execute-o `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#6)]
     [!code-vb[Trin_VstcoreExcelAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#6)]  
  
### <a name="to-save-the-active-workbook-in-a-vsto-add-in"></a>Para salvar a pasta de trabalho ativa em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Workbook.SaveCopyAs%2A> método para salvar uma cópia da pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#5](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#5)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#5](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#5)]  
  
## <a name="robust-programming"></a>Programação robusta  
 Cancelar interativamente qualquer um dos métodos que salvam ou copiar a pasta de trabalho gera um erro de tempo de execução em seu código. Por exemplo, se o procedimento chama o <xref:Microsoft.Office.Tools.Excel.Workbook.SaveAs%2A> método mas não desabilitar não solicita do Excel, e o usuário clicar em **Cancelar** quando solicitado, o Excel gera um erro de tempo de execução.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)   
 [Item de host da pasta de trabalho](../vsto/workbook-host-item.md)   
 [Como: Fechar pastas de trabalho de forma programática](../vsto/how-to-programmatically-close-workbooks.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  