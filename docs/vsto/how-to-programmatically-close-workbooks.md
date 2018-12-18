---
title: 'Como: Fechar pastas de trabalho de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, closing
- Excel [Office development in Visual Studio], closing workbooks
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 36b7da02830375161af08bda301e3ead98321741
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670191"
---
# <a name="how-to-programmatically-close-workbooks"></a>Como: Fechar pastas de trabalho de forma programática
  Você pode fechar a pasta de trabalho ativa ou você pode especificar uma pasta de trabalho para fechar.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="close-the-active-workbook"></a>Feche a pasta de trabalho do Active Directory  
 Há dois procedimentos para fechar a pasta de trabalho ativa: um para personalizações no nível de documento e outro para suplementos do VSTO.  
  
### <a name="to-close-the-active-workbook-in-a-document-level-customization"></a>Para fechar a pasta de trabalho ativa em uma personalização no nível de documento  
  
1.  Chamar o <xref:Microsoft.Office.Tools.Excel.Workbook.Close%2A> método para fechar a pasta de trabalho associada com a personalização. Para usar o exemplo de código a seguir, execute-o `Sheet1` classe em um projeto de nível de documento para Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#3](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#3)]
     [!code-vb[Trin_VstcoreExcelAutomation#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#3)]  
  
### <a name="to-close-the-active-workbook-in-a-vsto-add-in"></a>Para fechar a pasta de trabalho ativa em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Workbook.Close%2A> método para fechar a pasta de trabalho ativa. Para usar o exemplo de código a seguir, execute-o `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#1](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#1)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#1](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#1)]  
  
## <a name="close-a-workbook-that-you-specify-by-name"></a>Fechar uma pasta de trabalho que você especifica por nome  
 A maneira que você fechar uma pasta de trabalho que você especifica por nome é o mesmo para suplementos do VSTO e personalizações no nível do documento.  
  
### <a name="to-close-a-workbook-that-you-specify-by-name"></a>Para fechar uma pasta de trabalho que você especifica por nome  
  
1.  Especifique o nome de pasta de trabalho como um argumento para o <xref:Microsoft.Office.Interop.Excel.Workbooks> coleção. O exemplo de código a seguir pressupõe que uma pasta de trabalho denominada **NewWorkbook** está aberta no Excel.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#2](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#2)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#2](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#2)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)   
 [Como: salvar pastas de trabalho de forma programática](../vsto/how-to-programmatically-save-workbooks.md)   
 [Como: abrir pastas de trabalho de forma programática](../vsto/how-to-programmatically-open-workbooks.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  