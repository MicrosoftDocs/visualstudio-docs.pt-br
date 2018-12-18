---
title: 'Como: remover todos os comentários de documentos programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], removing comments
- comments, removing from documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 005414fce7b7bc04c22b266f5f5f6d54a399a182
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670096"
---
# <a name="how-to-programmatically-remove-all-comments-from-documents"></a>Como: remover todos os comentários de documentos programaticamente
  Use o `DeleteAllComments` método para remover todos os comentários de um documento do Microsoft Office Word.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-remove-all-comments-from-a-document-that-is-part-of-a-document-level-customization"></a>Para remover todos os comentários de um documento que faz parte de uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Word.Document.DeleteAllComments%2A> método da `ThisDocument` classe em seu projeto. Para usar este exemplo de código, executá-la na `ThisDocument` classe.  
  
     [!code-vb[Trin_VstcoreWordAutomation#119](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#119)]
     [!code-csharp[Trin_VstcoreWordAutomation#119](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#119)]  
  
## <a name="to-remove-all-comments-from-a-document-by-using-a-vsto-add-in"></a>Para remover todos os comentários de um documento usando um suplemento do VSTO  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word._Document.DeleteAllComments%2A> método da <xref:Microsoft.Office.Interop.Word.Document> da qual você deseja remover comentários.  
  
     O exemplo de código a seguir remove todos os comentários do documento ativo. Para usar este exemplo de código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#119](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#119)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#119](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#119)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: adicionar comentários ao texto em documentos de forma programática](../vsto/how-to-programmatically-add-comments-to-text-in-documents.md)   
 [Item de host do documento](../vsto/document-host-item.md)  
  
  