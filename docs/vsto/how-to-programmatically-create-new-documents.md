---
title: Como criar programaticamente novos documentos
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], custom document
- Word [Office development in Visual Studio], creating documents
- documents [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8e82c5ca62c407481b73de9394c584c3039a8f57
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545984"
---
# <a name="how-to-programmatically-create-new-documents"></a>Como criar programaticamente novos documentos
  Quando você cria um documento programaticamente, o novo documento é um <xref:Microsoft.Office.Interop.Word.Document> objeto nativo. Este objeto não tem os recursos adicionais de associação de dados e eventos de um <xref:Microsoft.Office.Tools.Word.Document> item de host. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Ao desenvolver um projeto de nível de documento, você não pode adicionar <xref:Microsoft.Office.Tools.Word.Document> itens de host programaticamente ao seu projeto. Em um projeto de suplemento do VSTO, você pode converter qualquer <xref:Microsoft.Office.Interop.Word.Document> objeto em um <xref:Microsoft.Office.Tools.Word.Document> item de host em tempo de execução. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>Para criar um novo documento com base no modelo normal

- Use o <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Documents> coleção para criar um novo documento com base no modelo normal. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#1)]
     [!code-csharp[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#1)]

## <a name="use-custom-templates"></a>Usar modelos personalizados
 O <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método tem um argumento de *modelo* opcional para criar um novo documento com base em um modelo diferente do modelo normal. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do modelo.

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>Para criar um novo documento com base em um modelo personalizado

- Chame o <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Documents> coleção e especifique o caminho para o modelo. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#2)]
     [!code-csharp[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#2)]

## <a name="see-also"></a>Confira também
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
