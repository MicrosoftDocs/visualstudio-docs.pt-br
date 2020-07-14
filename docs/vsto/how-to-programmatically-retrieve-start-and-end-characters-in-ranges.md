---
title: Comece a & caracteres finais em intervalos programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, retrieving start and end characters
- end characters
- start characters
- documents [Office development in Visual Studio], retrieving ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 485945f235a9161b6dc0584f7018c6f03c6024f5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537651"
---
# <a name="how-to-programmatically-retrieve-start-and-end-characters-in-ranges"></a>Como recuperar programaticamente caracteres de início e término em intervalos
  Este exemplo demonstra como você pode recuperar as posições de caracteres das posições inicial e final de um intervalo.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-retrieve-start-and-end-characters-of-a-range-in-a-document-level-customization"></a>Para recuperar os caracteres inicial e final de um intervalo em uma personalização no nível do documento

1. Obter os valores das <xref:Microsoft.Office.Interop.Word.Range.Start%2A> Propriedades e <xref:Microsoft.Office.Interop.Word.Range.End%2A> do <xref:Microsoft.Office.Interop.Word.Range> objeto. O exemplo de código a seguir obtém a posição inicial e final da segunda sentença no documento. Para usar este exemplo de código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#25)]
     [!code-csharp[Trin_VstcoreWordAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#25)]

## <a name="to-retrieve-start-and-end-characters-of-a-range-by-using-a-vsto-add-in"></a>Para recuperar os caracteres inicial e final de um intervalo usando um suplemento do VSTO

1. Obter os valores das <xref:Microsoft.Office.Interop.Word.Range.Start%2A> Propriedades e <xref:Microsoft.Office.Interop.Word.Range.End%2A> do <xref:Microsoft.Office.Interop.Word.Range> objeto. O exemplo de código a seguir obtém a posição inicial e final da segunda sentença no documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#25)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#25](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#25)]

## <a name="see-also"></a>Consulte também
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [Como: contar caracteres programaticamente em documentos](../vsto/how-to-programmatically-count-characters-in-documents.md)
