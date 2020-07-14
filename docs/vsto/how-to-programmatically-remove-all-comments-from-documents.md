---
title: 'Como: remover programaticamente todos os comentários de documentos'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], removing comments
- comments, removing from documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4b2b0e2be92ca5d4b548b297d01f8ec31b779510
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519880"
---
# <a name="how-to-programmatically-remove-all-comments-from-documents"></a>Como: remover programaticamente todos os comentários de documentos
  Use o `DeleteAllComments` método para remover todos os comentários de um Microsoft Office documento do Word.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-remove-all-comments-from-a-document-that-is-part-of-a-document-level-customization"></a>Para remover todos os comentários de um documento que faz parte de uma personalização em nível de documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.DeleteAllComments%2A> método da `ThisDocument` classe em seu projeto. Para usar este exemplo de código, execute-o da `ThisDocument` classe.

     [!code-vb[Trin_VstcoreWordAutomation#119](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#119)]
     [!code-csharp[Trin_VstcoreWordAutomation#119](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#119)]

## <a name="to-remove-all-comments-from-a-document-by-using-a-vsto-add-in"></a>Para remover todos os comentários de um documento usando um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.DeleteAllComments%2A> método do <xref:Microsoft.Office.Interop.Word.Document> qual você deseja remover comentários.

     O exemplo de código a seguir remove todos os comentários do documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#119](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#119)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#119](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#119)]

## <a name="see-also"></a>Confira também
- [Como: adicionar comentários ao texto de forma programática em documentos](../vsto/how-to-programmatically-add-comments-to-text-in-documents.md)
- [Item de host do documento](../vsto/document-host-item.md)
