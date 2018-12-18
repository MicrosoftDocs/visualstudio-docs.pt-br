---
title: 'Como: adicionar comentários ao texto em documentos de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- comments, adding to documents
- documents [Office development in Visual Studio], adding comments
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ca0d15ee69bb58aae765c03c1233a78bfeeb119c
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669802"
---
# <a name="how-to-programmatically-add-comments-to-text-in-documents"></a>Como: adicionar comentários ao texto em documentos de forma programática
  A propriedade de comentários da classe Document adiciona um comentário a um intervalo de texto em um documento do Microsoft Office Word.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 O exemplo a seguir adiciona um comentário ao primeiro parágrafo no documento.  
  
## <a name="to-add-a-new-comment-to-text-in-a-document-level-customization"></a>Para adicionar um novo comentário ao texto em uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> método da <xref:Microsoft.Office.Tools.Word.Document.Comments%2A> propriedade e forneça um intervalo e o texto do comentário. Para usar o exemplo de código a seguir, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#118](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#118)]
     [!code-csharp[Trin_VstcoreWordAutomation#118](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#118)]  
  
## <a name="to-add-a-new-comment-to-text-in-a-vsto-add-in"></a>Para adicionar um novo comentário ao texto em um suplemento do VSTO  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> método da <xref:Microsoft.Office.Interop.Word._Document.Comments%2A> propriedade e forneça um intervalo e o texto do comentário.  
  
     O exemplo de código a seguir adiciona um comentário ao documento ativo. Para usar este exemplo, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#118](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#118)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#118](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#118)]  
  
## <a name="robust-programming"></a>Programação robusta  
 Para alterar as iniciais do usuário que o Word adiciona comentários, use o <xref:Microsoft.Office.Interop.Word._Application.UserInitials%2A> propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Como: remover todos os comentários de documentos programaticamente](../vsto/how-to-programmatically-remove-all-comments-from-documents.md)   
 [Item de host do documento](../vsto/document-host-item.md)  
  
  