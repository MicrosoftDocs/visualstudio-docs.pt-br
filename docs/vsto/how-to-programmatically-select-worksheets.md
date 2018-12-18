---
title: 'Como: Selecionar planilhas programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, selecting
- Excel projects, selecting worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 09e477d802b9d92ca4f9e1cd3a532145ad0e68a0
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670760"
---
# <a name="how-to-programmatically-select-worksheets"></a>Como: Selecionar planilhas programaticamente
  O <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> método seleciona o objeto especificado, que move a seleção do usuário para o novo objeto. Use o <xref:Microsoft.Office.Tools.Excel.Worksheet.Activate%2A> método se você deseja colocar o foco para o objeto sem alterar a seleção do usuário.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Se você deseja selecionar uma planilha existente em um suplemento do VSTO ou se a planilha foi criada em tempo de execução em uma personalização no nível de documento, você deverá acessá-lo usando o Excel <xref:Microsoft.Office.Interop.Excel.Sheets> coleção de pasta de trabalho do Excel; caso contrário, você pode acessar o <xref:Microsoft.Office.Tools.Excel.Worksheet>item de host diretamente.  
  
## <a name="use-the-worksheet-host-item"></a>Use o item de host da planilha  
 Em uma personalização no nível de documento, adicione o seguinte código ao *Sheet1.vb* ou *Sheet1.cs*.  
  
### <a name="to-select-the-first-worksheet-in-a-workbook-using-a-host-item"></a>Para selecionar a primeira planilha em uma pasta de trabalho usando um item de host  
  
1.  Chame o método <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> de `Sheet1`.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#19)]
     [!code-vb[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#19)]  
  
## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção de planilhas da pasta de trabalho do Excel  
 Acessar a planilha usando o Excel <xref:Microsoft.Office.Interop.Excel.Sheets> coleção.  
  
### <a name="to-select-the-first-worksheet-in-a-workbook-using-the-sheets-collection-of-the-excel-workbook"></a>Para selecionar a primeira planilha em uma pasta de trabalho usando a coleção de planilhas da pasta de trabalho do Excel  
  
1.  Chame o <xref:Microsoft.Office.Interop.Excel.Sheets.Select%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção para selecionar a primeira planilha da pasta de trabalho ativa.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#20)]
     [!code-vb[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#20)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: Imprimir planilhas programaticamente](../vsto/how-to-programmatically-print-worksheets.md)   
 [Como: excluir planilhas de pastas de trabalho de forma programática](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)   
 [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)   
 [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)   
 [Item de host da planilha](../vsto/worksheet-host-item.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  