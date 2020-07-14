---
title: 'Como: adicionar cabeçalhos e rodapés programaticamente a documentos'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- headers, adding to Office documents
- documents [Office development in Visual Studio], adding headers
- documents [Office development in Visual Studio], adding footers
- footers, adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52724103df17a1eaaf364f255f127a576beda798
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519919"
---
# <a name="how-to-programmatically-add-headers-and-footers-to-documents"></a>Como: adicionar cabeçalhos e rodapés programaticamente a documentos
  Você pode adicionar texto a cabeçalhos e rodapés no documento usando a <xref:Microsoft.Office.Interop.Word.Section.Headers%2A> propriedade e a <xref:Microsoft.Office.Interop.Word.Section.Footers%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Section> . Cada seção de um documento contém três cabeçalhos e rodapés:

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterPrimary>

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterEvenPages>

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterFirstPage>

  Os procedimentos são diferentes para as personalizações em nível de documento e os suplementos do VSTO.

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="document-level-customizations"></a>Personalizações no nível de documento
 Para usar os exemplos de código a seguir, execute-os a partir da `ThisDocument` classe em seu projeto.

### <a name="to-add-text-to-footers-in-the-document"></a>Para adicionar texto a rodapés no documento

1. O exemplo de código a seguir define a fonte do texto a ser inserido no rodapé principal de cada seção do documento e insere o texto no rodapé.

     [!code-vb[Trin_VstcoreWordAutomation#114](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#114)]
     [!code-csharp[Trin_VstcoreWordAutomation#114](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#114)]

### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos no documento

1. O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento do parágrafo para que o texto fique alinhado à direita do cabeçalho.

     [!code-vb[Trin_VstcoreWordAutomation#116](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#116)]
     [!code-csharp[Trin_VstcoreWordAutomation#116](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#116)]

## <a name="vsto-add-ins"></a>Suplementos do VSTO
 Para usar os exemplos de código a seguir, execute-os a partir da `ThisAddIn` classe em seu projeto.

### <a name="to-add-text-to-footers-in-a-document"></a>Para adicionar texto a rodapés em um documento

1. O exemplo de código a seguir define a fonte do texto a ser inserido no rodapé principal de cada seção do documento e insere o texto no rodapé. Este exemplo de código usa o documento ativo.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#114](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#114)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#114](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#114)]

### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos no documento

1. O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento do parágrafo para que o texto fique alinhado à direita do cabeçalho. Este exemplo de código usa o documento ativo.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#116](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#116)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#116](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#116)]

## <a name="see-also"></a>Confira também
- [Como criar programaticamente novos documentos](../vsto/how-to-programmatically-create-new-documents.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como fazer loops programaticamente por meio de itens encontrados em documentos](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
