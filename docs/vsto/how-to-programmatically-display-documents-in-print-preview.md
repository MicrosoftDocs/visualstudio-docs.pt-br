---
title: Como exibir programaticamente documentos na visualização de impressão
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], displaying documents in print preview
- documents [Office development in Visual Studio], displaying in print preview
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 036f8a45d5605b55b9743a22d598a13780641c97
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545906"
---
# <a name="how-to-programmatically-display-documents-in-print-preview"></a>Como exibir programaticamente documentos na visualização de impressão
  Se sua solução gerar um relatório, talvez você queira exibir o relatório para o usuário no modo de visualização de impressão.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="procedures-for-document-level-customizations"></a>Procedimentos para personalizações em nível de documento

### <a name="to-display-a-document-in-print-preview-by-calling-the-printpreview-method"></a>Para exibir um documento na visualização de impressão chamando o método Print Preview

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.PrintPreview%2A> método da <xref:Microsoft.Office.Tools.Word.Document> classe. Para usar este exemplo de código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#13)]
     [!code-csharp[Trin_VstcoreWordAutomation#13](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#13)]

### <a name="to-display-a-document-in-print-preview-by-setting-the-printpreview-property"></a>Para exibir um documento na visualização de impressão definindo a propriedade Print Preview

1. Defina a <xref:Microsoft.Office.Interop.Word._Application.PrintPreview%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Application> objeto como **true**.

     [!code-vb[Trin_VstcoreWordAutomation#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#14)]
     [!code-csharp[Trin_VstcoreWordAutomation#14](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#14)]

## <a name="procedures-for-vsto-add-ins"></a>Procedimentos para suplementos do VSTO

### <a name="to-display-a-document-in-print-preview-by-calling-the-printpreview-method"></a>Para exibir um documento na visualização de impressão chamando o método Print Preview

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.PrintPreview%2A> método do <xref:Microsoft.Office.Interop.Word.Document> que você deseja visualizar. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#13](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#13)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#13](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#13)]

### <a name="to-display-a-document-in-print-preview-by-setting-the-printpreview-property"></a>Para exibir um documento na visualização de impressão definindo a propriedade Print Preview

1. Defina a <xref:Microsoft.Office.Interop.Word._Application.PrintPreview%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Application> objeto como **true**.

     [!code-vb[Trin_VstcoreWordAutomation#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#14)]
     [!code-csharp[Trin_VstcoreWordAutomation#14](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#14)]

## <a name="see-also"></a>Confira também
- [Como: imprimir documentos programaticamente](../vsto/how-to-programmatically-print-documents.md)
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Como criar programaticamente novos documentos](../vsto/how-to-programmatically-create-new-documents.md)
