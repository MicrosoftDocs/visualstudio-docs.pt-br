---
title: 'Como: ocultar planilhas programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a60a0189af5608496e1f0f415a2d668e896af8e3
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670724"
---
# <a name="how-to-programmatically-hide-worksheets"></a>Como: ocultar planilhas programaticamente
  Você pode mostrar ou ocultar qualquer planilha em uma pasta de trabalho. Para ocultar uma planilha, use o item de host da planilha ou acessar a planilha usando a coleção de planilhas da pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="use-the-worksheet-host-item"></a>Use o item de host da planilha  
 Se a planilha foi adicionada em tempo de design em uma personalização no nível de documento, use o <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> propriedade para ocultar a planilha especificada.  
  
### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>Para ocultar uma planilha usando um item de host da planilha  
  
1.  Defina a <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> propriedade do `Sheet1` item de host para o <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> valor de enumeração.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#25)]  
  
## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção de planilhas da pasta de trabalho do Excel  
 Acessar planilhas por meio do Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> coleção nos seguintes casos:  
  
-   Você deseja ocultar uma planilha em um suplemento do VSTO.  
  
-   A planilha que você deseja ocultar foi criada em tempo de execução em uma personalização no nível de documento.  
  
### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>Para ocultar uma planilha usando a coleção de planilhas da pasta de trabalho do Excel  
  
1.  Defina as <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> propriedade da planilha para o <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> valor de enumeração.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#26)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: excluir planilhas de pastas de trabalho de forma programática](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)   
 [Como: mover planilhas em pastas de trabalho de forma programática](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)   
 [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)  
  