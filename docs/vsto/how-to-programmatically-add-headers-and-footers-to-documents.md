---
title: 'Como: adicionar cabeçalhos e rodapés programaticamente a documentos'
description: Saiba como você pode adicionar texto a cabeçalhos e rodapés no documento usando a propriedade Headers e os rodapés da seção.
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 73844d19ef6bb85c623706ab0d359836e42a3b14
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828731"
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

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet114":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet114":::

### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos no documento

1. O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento do parágrafo para que o texto fique alinhado à direita do cabeçalho.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet116":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet116":::

## <a name="vsto-add-ins"></a>Suplementos do VSTO
 Para usar os exemplos de código a seguir, execute-os a partir da `ThisAddIn` classe em seu projeto.

### <a name="to-add-text-to-footers-in-a-document"></a>Para adicionar texto a rodapés em um documento

1. O exemplo de código a seguir define a fonte do texto a ser inserido no rodapé principal de cada seção do documento e insere o texto no rodapé. Este exemplo de código usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet114":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet114":::

### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos no documento

1. O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento do parágrafo para que o texto fique alinhado à direita do cabeçalho. Este exemplo de código usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet116":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet116":::

## <a name="see-also"></a>Consulte também
- [Como criar programaticamente novos documentos](../vsto/how-to-programmatically-create-new-documents.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como fazer loops programaticamente por meio de itens encontrados em documentos](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
