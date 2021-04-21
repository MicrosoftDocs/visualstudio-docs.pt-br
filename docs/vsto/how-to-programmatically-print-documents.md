---
title: 'Como: imprimir documentos programaticamente'
description: Saiba como você pode imprimir um documento inteiro do Microsoft Word ou parte de um documento, em sua impressora padrão.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], printing documents
- documents [Office development in Visual Studio], printing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 47f295a6259b8d722c9c3c714b62fe648bdea1c6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827195"
---
# <a name="how-to-programmatically-print-documents"></a>Como: imprimir documentos programaticamente
  Você pode imprimir um documento do Word Microsoft Office inteiro ou parte de um documento, em sua impressora padrão.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="print-a-document-that-is-part-of-a-document-level-customization"></a>Imprimir um documento que faz parte de uma personalização no nível do documento

### <a name="to-print-the-entire-document"></a>Para imprimir o documento inteiro

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.PrintOut%2A> método da `ThisDocument` classe em seu projeto para imprimir o documento inteiro. Para usar esse exemplo, execute o código na classe `ThisDocument`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet11":::

### <a name="to-print-the-current-page-of-the-document"></a>Para imprimir a página atual do documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.PrintOut%2A> método da `ThisDocument` classe em seu projeto e especifique que uma cópia da página atual seja impressa. Para usar esse exemplo, execute o código na classe `ThisDocument`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet12":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet12":::

## <a name="print-a-document-by-using-a-vsto-add-in"></a>Imprimir um documento usando um suplemento do VSTO

### <a name="to-print-an-entire-document"></a>Para imprimir um documento inteiro

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.PrintOut%2A> método do <xref:Microsoft.Office.Interop.Word.Document> objeto que você deseja imprimir. O exemplo de código a seguir imprime o documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet11":::

### <a name="to-print-the-current-page-of-a-document"></a>Para imprimir a página atual de um documento

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.PrintOut%2A> método do <xref:Microsoft.Office.Interop.Word.Document> objeto que você deseja imprimir e especifique que uma cópia da página atual seja impressa. O exemplo de código a seguir imprime o documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet12":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet12":::

## <a name="see-also"></a>Consulte também
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
