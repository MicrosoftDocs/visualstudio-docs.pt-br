---
title: Como criar programaticamente novos documentos
description: Saiba como você pode criar programaticamente novos documentos no Microsoft Word usando o Visual Studio.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4ba9aed0194804354af62fb1fd582b8ea12ac6b1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825180"
---
# <a name="how-to-programmatically-create-new-documents"></a>Como criar programaticamente novos documentos
  Quando você cria um documento programaticamente, o novo documento é um <xref:Microsoft.Office.Interop.Word.Document> objeto nativo. Este objeto não tem os recursos adicionais de associação de dados e eventos de um <xref:Microsoft.Office.Tools.Word.Document> item de host. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Ao desenvolver um projeto de nível de documento, você não pode adicionar <xref:Microsoft.Office.Tools.Word.Document> itens de host programaticamente ao seu projeto. Em um projeto de suplemento do VSTO, você pode converter qualquer <xref:Microsoft.Office.Interop.Word.Document> objeto em um <xref:Microsoft.Office.Tools.Word.Document> item de host em tempo de execução. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>Para criar um novo documento com base no modelo normal

- Use o <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Documents> coleção para criar um novo documento com base no modelo normal. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet1":::

## <a name="use-custom-templates"></a>Usar modelos personalizados
 O <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método tem um argumento de *modelo* opcional para criar um novo documento com base em um modelo diferente do modelo normal. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do modelo.

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>Para criar um novo documento com base em um modelo personalizado

- Chame o <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Documents> coleção e especifique o caminho para o modelo. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet2":::

## <a name="see-also"></a>Consulte também
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
