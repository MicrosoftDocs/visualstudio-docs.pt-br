---
title: 'Como: adicionar programaticamente os cabeçalhos e rodapés a documentos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- headers, adding to Office documents
- documents [Office development in Visual Studio], adding headers
- documents [Office development in Visual Studio], adding footers
- footers, adding to documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cf8fd8d679760a6758ffb4afb71262a897845e87
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849899"
---
# <a name="how-to-programmatically-add-headers-and-footers-to-documents"></a>Como: adicionar programaticamente os cabeçalhos e rodapés a documentos
  Você pode adicionar texto aos cabeçalhos e rodapés do documento usando o <xref:Microsoft.Office.Interop.Word.Section.Headers%2A> propriedade e <xref:Microsoft.Office.Interop.Word.Section.Footers%2A> propriedade do <xref:Microsoft.Office.Interop.Word.Section>. Cada seção de um documento contém três cabeçalhos e rodapés de páginas:  
  
- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterPrimary>  
  
- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterEvenPages>  
  
- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterFirstPage>  
  
  Os procedimentos são diferentes para personalizações no nível de documento e suplementos do VSTO.  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="document-level-customizations"></a>Personalizações no nível de documento  
 Para usar os exemplos de código a seguir, executá-los pelo `ThisDocument` classe em seu projeto.  
  
### <a name="to-add-text-to-footers-in-the-document"></a>Para adicionar texto ao rodapés do documento  
  
1.  O exemplo de código a seguir define a fonte do texto a ser inserido no rodapé de cada seção do documento principal e, em seguida, insere texto no rodapé.  
  
     [!code-vb[Trin_VstcoreWordAutomation#114](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#114)]
     [!code-csharp[Trin_VstcoreWordAutomation#114](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#114)]  
  
### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos do documento  
  
1.  O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento de parágrafo para que o texto é alinhado à direita do cabeçalho.  
  
     [!code-vb[Trin_VstcoreWordAutomation#116](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#116)]
     [!code-csharp[Trin_VstcoreWordAutomation#116](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#116)]  
  
## <a name="vsto-add-ins"></a>Suplementos do VSTO  
 Para usar os exemplos de código a seguir, executá-los pelo `ThisAddIn` classe em seu projeto.  
  
### <a name="to-add-text-to-footers-in-a-document"></a>Para adicionar texto ao rodapés de páginas em um documento  
  
1.  O exemplo de código a seguir define a fonte do texto a ser inserido no rodapé de cada seção do documento principal e, em seguida, insere texto no rodapé. Este exemplo de código usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#114](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#114)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#114](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#114)]  
  
### <a name="to-add-text-to-headers-in-the-document"></a>Para adicionar texto aos cabeçalhos do documento  
  
1.  O exemplo de código a seguir adiciona um campo para mostrar o número da página em cada cabeçalho no documento e, em seguida, define o alinhamento de parágrafo para que o texto é alinhado à direita do cabeçalho. Este exemplo de código usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#116](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#116)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#116](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#116)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar novos documentos programaticamente](../vsto/how-to-programmatically-create-new-documents.md)   
 [Como: estender programaticamente os intervalos em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)   
 [Como: executar um loop por meio de itens encontrados em documentos programaticamente](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)  
   