---
title: 'Como: usar programaticamente caixas de diálogo internas no Word'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c3273b22d98be1c22cf0c8cea2cb57e277b9b48
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537612"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>Como: usar programaticamente caixas de diálogo internas no Word
  Ao trabalhar com o Microsoft Office Word, há ocasiões em que você precisa exibir caixas de diálogo para entrada do usuário. Embora você possa criar o seu próprio, talvez também queira adotar a abordagem de uso das caixas de diálogo internas do Word, que são expostas na <xref:Microsoft.Office.Interop.Word.Dialogs> coleção do <xref:Microsoft.Office.Interop.Word.Application> objeto. Isso permite que você acesse mais de 200 das caixas de diálogo internas, que são representadas como enumerações.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>Exibir caixas de diálogo
 Para exibir uma caixa de diálogo, use um dos valores da <xref:Microsoft.Office.Interop.Word.WdWordDialog> enumeração para criar um <xref:Microsoft.Office.Interop.Word.Dialog> objeto que represente a caixa de diálogo que você deseja exibir. Em seguida, chame o <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> método do <xref:Microsoft.Office.Interop.Word.Dialog> objeto.

 O exemplo de código a seguir demonstra como exibir a caixa de diálogo **Abrir arquivo** . Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou no seu projeto.

 [!code-vb[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#100)]
 [!code-csharp[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#100)]

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>Acessar membros da caixa de diálogo que estão disponíveis por meio da associação tardia
 Algumas propriedades e métodos de caixas de diálogo no Word estão disponíveis somente por meio da associação tardia. Em projetos de Visual Basic em que **Option Strict** está on, você deve usar Reflection para acessar esses membros. Para obter mais informações, consulte [associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md).

 O exemplo de código a seguir demonstra como usar a propriedade **Name** da caixa de diálogo **File Open** em Visual Basic projetos em que **Option Strict** está off ou em projetos do Visual C# direcionados para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] . Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou no seu projeto.

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 O exemplo de código a seguir demonstra como usar a reflexão para acessar a propriedade **Name** da caixa de diálogo **arquivo abrir** em projetos de Visual Basic em que **Option Strict** está on. Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou no seu projeto.

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>Consulte também
- [Como: usar de forma programática as caixas de diálogo do Word no modo oculto](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Instrução Option Strict](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [Reflexão (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [Reflexão (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
