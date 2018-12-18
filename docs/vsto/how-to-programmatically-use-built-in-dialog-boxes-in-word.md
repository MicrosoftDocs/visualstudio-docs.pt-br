---
title: 'Como: usar as caixas de diálogo integradas no Word de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f5ee28b0296037b9b5490ca691a27d613c793228
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669971"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>Como: usar as caixas de diálogo integradas no Word de forma programática
  Ao trabalhar com o Microsoft Office Word, há ocasiões em que você precisa para exibir caixas de diálogo para entrada do usuário. Embora você possa criar seus próprios, você também poderá usar a abordagem do uso de caixas de diálogo integradas no Word, que são expostas na <xref:Microsoft.Office.Interop.Word.Dialogs> coleção do <xref:Microsoft.Office.Interop.Word.Application> objeto. Isso permite que você acesse mais de 200 caixas de diálogo internas, que são representadas como enumerações.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="display-dialog-boxes"></a>Exibir caixas de diálogo  
 Para exibir uma caixa de diálogo, use um dos valores da <xref:Microsoft.Office.Interop.Word.WdWordDialog> enumeração para criar um <xref:Microsoft.Office.Interop.Word.Dialog> objeto que representa a caixa de diálogo que você deseja exibir. Em seguida, chame o <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> método da <xref:Microsoft.Office.Interop.Word.Dialog> objeto.  
  
 O exemplo de código a seguir demonstra como exibir o **abrir arquivo** caixa de diálogo. Para usar este exemplo, executá-la na `ThisDocument` ou `ThisAddIn` classe em seu projeto.  
  
 [!code-vb[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#100)]
 [!code-csharp[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#100)]  
  
### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>Acessar membros de caixa de diálogo que estão disponíveis por meio de associação tardia  
 Algumas propriedades e métodos de caixas de diálogo do Word estão disponíveis apenas por meio de associação tardia. No Visual Basic, projetos where **Option Strict** estiver ativado, você deve usar a reflexão para acessar esses membros. Para obter mais informações, consulte [associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md).  
  
 O exemplo de código a seguir demonstra como usar o **nome** propriedade da **abrir arquivo** caixa de diálogo no Visual Basic projetos where **Option Strict** está desligado de propriedades ou no Visual c# projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. Para usar este exemplo, executá-la na `ThisDocument` ou `ThisAddIn` classe em seu projeto.  
  
 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]  
  
 O exemplo de código a seguir demonstra como usar reflexão para acessar o **nome** propriedade da **abrir arquivo** caixa de diálogo no Visual Basic projetos where **Option Strict** é no. Para usar este exemplo, executá-la na `ThisDocument` ou `ThisAddIn` classe em seu projeto.  
  
 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: usar caixas de diálogo do Word no modo oculto de forma programática](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)   
 [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Instrução Option strict](/dotnet/visual-basic/language-reference/statements/option-strict-statement)   
 [Reflexão (C#)](/dotnet/csharp/programming-guide/concepts/reflection)  
 [Reflexão (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)  
  
  