---
title: 'Como: usar de forma programática as caixas de diálogo do Word no modo oculto'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 923fc7ddec0350f254968fe17494ecbe27f76b13
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537573"
---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>Como: usar de forma programática as caixas de diálogo do Word no modo oculto
  Você pode executar operações complexas com uma chamada de método invocando as caixas de diálogo internas no Microsoft Office Word sem exibi-las ao usuário. Você pode fazer isso usando o <xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A> método do <xref:Microsoft.Office.Interop.Word.Dialog> objeto sem chamar o <xref:Microsoft.Office.Interop.Word.Dialog.Display%2A> método.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="examples"></a>Exemplos
 Os exemplos de código a seguir demonstram como usar a caixa de diálogo **configuração de página** no modo oculto para definir várias propriedades de configuração de página sem entrada do usuário. Os exemplos usam um <xref:Microsoft.Office.Interop.Word.Dialog> objeto para configurar um tamanho de página personalizado. As configurações específicas para a configuração de página, como a margem superior, a margem inferior e assim por diante, estão disponíveis como propriedades de associação tardia do <xref:Microsoft.Office.Interop.Word.Dialog> objeto. Essas propriedades são criadas dinamicamente pelo Word em tempo de execução.

 O exemplo a seguir demonstra como executar essa tarefa em projetos Visual Basic em que **Option Strict** é off e em projetos do Visual C# direcionados para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] . Nesses projetos, você pode usar os recursos de associação tardia nos compiladores Visual Basic e Visual C#. Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou no seu projeto.

 [!code-vb[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#123)]
 [!code-csharp[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#123)]

 O exemplo a seguir demonstra como executar essa tarefa em projetos Visual Basic em que **Option Strict** está on. Nesses projetos, você deve usar a reflexão para acessar as propriedades de associação tardia. Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou no seu projeto.

 [!code-vb[Trin_VstcoreWordAutomation#104](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#104)]

## <a name="see-also"></a>Confira também
- [Como: usar programaticamente caixas de diálogo internas no Word](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md)
- [Reflexão (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [Reflexão (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
