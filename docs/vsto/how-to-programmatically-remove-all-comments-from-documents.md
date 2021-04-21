---
title: 'Como: remover programaticamente todos os comentários de documentos'
description: Saiba como você pode usar o Visual Studio para remover programaticamente todos os comentários de um documento do Microsoft Word.
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5d51f44537c4e9564162d458c564dd428e57d154
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827039"
---
# <a name="how-to-programmatically-remove-all-comments-from-documents"></a>Como: remover programaticamente todos os comentários de documentos
  Use o `DeleteAllComments` método para remover todos os comentários de um Microsoft Office documento do Word.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-remove-all-comments-from-a-document-that-is-part-of-a-document-level-customization"></a>Para remover todos os comentários de um documento que faz parte de uma personalização em nível de documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.DeleteAllComments%2A> método da `ThisDocument` classe em seu projeto. Para usar este exemplo de código, execute-o da `ThisDocument` classe.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet119":::

## <a name="to-remove-all-comments-from-a-document-by-using-a-vsto-add-in"></a>Para remover todos os comentários de um documento usando um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.DeleteAllComments%2A> método do <xref:Microsoft.Office.Interop.Word.Document> qual você deseja remover comentários.

     O exemplo de código a seguir remove todos os comentários do documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet119":::

## <a name="see-also"></a>Consulte também
- [Como: adicionar comentários ao texto de forma programática em documentos](../vsto/how-to-programmatically-add-comments-to-text-in-documents.md)
- [Item de host do documento](../vsto/document-host-item.md)
