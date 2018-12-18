---
title: 'Como: criar programaticamente novas pastas de trabalho'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], creating workbooks
- workbooks, creating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7e1da9ff331a4376a6ff242dca4382832ee4e85f
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257102"
---
# <a name="how-to-programmatically-create-new-workbooks"></a>Como: criar programaticamente novas pastas de trabalho
  Quando você cria uma pasta de trabalho por meio de programação, é um nativo <xref:Microsoft.Office.Interop.Excel.Workbook> do objeto, não um <xref:Microsoft.Office.Tools.Excel.Workbook> item de host.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Você pode gerar uma <xref:Microsoft.Office.Tools.Excel.Workbook> item de host para um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto no projeto do suplemento do VSTO. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="to-create-a-new-workbook"></a>Para criar uma nova pasta de trabalho  
  
1.  Use o <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> método da <xref:Microsoft.Office.Interop.Excel.Workbooks> coleção.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#1](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#1)]
     [!code-vb[Trin_VstcoreExcelAutomation#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#1)]  
  
    > [!NOTE]  
    >  Você pode criar uma pasta de trabalho com base em um modelo que não seja o modelo padrão: passar o modelo que você deseja usar como um parâmetro para o <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> método.  
  
## <a name="see-also"></a>Consulte também  
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)   
 [Como: abrir pastas de trabalho de forma programática](../vsto/how-to-programmatically-open-workbooks.md)   
 [Como: salvar pastas de trabalho de forma programática](../vsto/how-to-programmatically-save-workbooks.md)   
 [Como: Fechar pastas de trabalho de forma programática](../vsto/how-to-programmatically-close-workbooks.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  