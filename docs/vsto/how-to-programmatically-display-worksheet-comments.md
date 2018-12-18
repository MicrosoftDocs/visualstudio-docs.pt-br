---
title: 'Como: exibir comentários em planilhas de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, comments
- comments, worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e8f4875e75562d9fa1f6d9cd4982ae2148e35a1c
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257680"
---
# <a name="how-to-programmatically-display-worksheet-comments"></a>Como: exibir comentários em planilhas de forma programática
  Programaticamente, você pode mostrar e ocultar comentários em planilhas do Microsoft Office Excel.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="to-display-all-comments-on-a-worksheet-in-a-document-level-customization"></a>Para exibir todos os comentários em uma planilha em uma personalização no nível de documento  
  
1.  Definir a <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> propriedade para **verdadeiro** se você desejar mostrar comentários; caso contrário **false**. Esse código deve ser colocado em uma classe de folha, não no `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#31)]
     [!code-vb[Trin_VstcoreExcelAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#31)]  
  
## <a name="to-display-all-comments-on-a-worksheet-in-an-application-level-vsto-add-in"></a>Para exibir todos os comentários em uma planilha em um suplemento do VSTO do nível de aplicativo  
  
1.  Definir a <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> propriedade para **verdadeiro** se você desejar mostrar comentários; caso contrário **false**.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#21](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#21)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#21](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#21)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: adicionar e excluir comentários em planilhas de programaticamente](../vsto/how-to-programmatically-add-and-delete-worksheet-comments.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  