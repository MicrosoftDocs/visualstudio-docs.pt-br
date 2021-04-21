---
title: 'Como: adicionar comentários ao texto de forma programática em documentos'
description: Adicione de forma programática comentários ao texto em documentos. A propriedade Comments da classe Document adiciona um comentário a um intervalo de texto em um documento do Microsoft Word.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- comments, adding to documents
- documents [Office development in Visual Studio], adding comments
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4e03f189f2236131308b8f9ea5d90c52ffa3147d
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825817"
---
# <a name="how-to-programmatically-add-comments-to-text-in-documents"></a>Como: adicionar comentários ao texto de forma programática em documentos
  A propriedade Comments da classe Document adiciona um comentário a um intervalo de texto em um Microsoft Office documento do Word.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 O exemplo a seguir adiciona um comentário ao primeiro parágrafo do documento.

## <a name="to-add-a-new-comment-to-text-in-a-document-level-customization"></a>Para adicionar um novo comentário ao texto em uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> método da <xref:Microsoft.Office.Tools.Word.Document.Comments%2A> propriedade e forneça um intervalo e o texto do comentário. Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet118":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet118":::

## <a name="to-add-a-new-comment-to-text-in-a-vsto-add-in"></a>Para adicionar um novo comentário ao texto em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> método da <xref:Microsoft.Office.Interop.Word._Document.Comments%2A> propriedade e forneça um intervalo e o texto do comentário.

     O exemplo de código a seguir adiciona um comentário ao documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet118":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet118":::

## <a name="robust-programming"></a>Programação robusta
 Para alterar as iniciais do usuário que o Word adiciona aos comentários, use a <xref:Microsoft.Office.Interop.Word._Application.UserInitials%2A> propriedade.

## <a name="see-also"></a>Consulte também
- [Como: remover programaticamente todos os comentários de documentos](../vsto/how-to-programmatically-remove-all-comments-from-documents.md)
- [Item de host do documento](../vsto/document-host-item.md)
