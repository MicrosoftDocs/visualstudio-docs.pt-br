---
title: 'Como: definir e selecionar intervalos de forma programática em documentos'
description: Saiba como você pode definir e selecionar intervalos de forma programática em documentos do Microsoft Word usando o objeto Range.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], selecting sentences
- documents [Office development in Visual Studio], ranges
- sentences, selecting in documents
- ranges, selecting in documents
- ranges, defining in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3a5dc0c7fb9f3e9a2b4a15447f81239db973c215
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825947"
---
# <a name="how-to-programmatically-define-and-select-ranges-in-documents"></a>Como: definir e selecionar intervalos de forma programática em documentos
  Você pode definir um intervalo em um Microsoft Office documento do Word usando um <xref:Microsoft.Office.Interop.Word.Range> objeto. Você pode selecionar o documento inteiro de várias maneiras, por exemplo, usando o <xref:Microsoft.Office.Interop.Word.Range.Select%2A> método do <xref:Microsoft.Office.Interop.Word.Range> objeto ou usando a propriedade content da <xref:Microsoft.Office.Tools.Word.Document> classe (em uma personalização no nível do documento) ou a <xref:Microsoft.Office.Interop.Word.Document> classe (em um suplemento do VSTO).

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="define-a-range"></a>Definir um intervalo
 O exemplo a seguir mostra como criar um novo <xref:Microsoft.Office.Interop.Word.Range> objeto que inclui os primeiros sete caracteres no documento ativo, incluindo caracteres não imprimíveis. Em seguida, ele seleciona o texto dentro do intervalo.

### <a name="to-define-a-range-in-a-document-level-customization"></a>Para definir um intervalo em uma personalização no nível do documento

1. Adicione o intervalo ao documento passando um caractere de início e de término para o <xref:Microsoft.Office.Tools.Word.Document.Range%2A> método da <xref:Microsoft.Office.Tools.Word.Document> classe. Para usar este exemplo de código, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet18":::

### <a name="to-define-a-range-by-using-a-vsto-add-in"></a>Para definir um intervalo usando um suplemento do VSTO

1. Adicione o intervalo ao documento passando um caractere de início e de término para o <xref:Microsoft.Office.Interop.Word._Document.Range%2A> método da <xref:Microsoft.Office.Interop.Word.Document> classe. O exemplo de código a seguir adiciona um intervalo ao documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet18":::

## <a name="select-a-range-in-a-document-level-customization"></a>Selecionar um intervalo em uma personalização no nível do documento
 Os exemplos a seguir mostram como selecionar o documento inteiro usando o <xref:Microsoft.Office.Interop.Word.Range.Select%2A> método de um <xref:Microsoft.Office.Interop.Word.Range> objeto ou usando a <xref:Microsoft.Office.Tools.Word.Document.Content%2A> propriedade da <xref:Microsoft.Office.Tools.Word.Document> classe.

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>Para selecionar o documento inteiro como um intervalo usando o método Select

1. Use o <xref:Microsoft.Office.Interop.Word.Range.Select%2A> método de um <xref:Microsoft.Office.Interop.Word.Range> que contém o documento inteiro. Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>Para selecionar o documento inteiro como um intervalo usando a propriedade Content

1. Use a <xref:Microsoft.Office.Tools.Word.Document.Content%2A> propriedade para definir um intervalo que abrange todo o documento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet20":::

   Você também pode usar os métodos e as propriedades de outros objetos para definir um intervalo.

### <a name="to-select-a-sentence-in-the-active-document"></a>Para selecionar uma frase no documento ativo

1. Defina o intervalo usando a <xref:Microsoft.Office.Interop.Word.Sentences> coleção. Use o índice da frase que você deseja selecionar.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet21":::

   Outra maneira de selecionar uma sentença é definir manualmente os valores inicial e final para o intervalo.

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>Para selecionar uma sentença definindo manualmente os valores inicial e final

1. Crie uma variável de intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet23":::

2. Verifique se há pelo menos duas frases no documento, defina os argumentos de *início* e *término* do intervalo e, em seguida, selecione o intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet24":::

## <a name="select-a-range-by-using-a-vsto-add-in"></a>Selecionar um intervalo usando um suplemento do VSTO
 Os exemplos a seguir mostram como selecionar o documento inteiro usando o <xref:Microsoft.Office.Interop.Word.Range.Select%2A> método de um <xref:Microsoft.Office.Interop.Word.Range> objeto ou usando a <xref:Microsoft.Office.Interop.Word._Document.Content%2A> propriedade da <xref:Microsoft.Office.Interop.Word.Document> classe.

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>Para selecionar o documento inteiro como um intervalo usando o método Select

1. Use o <xref:Microsoft.Office.Interop.Word.Range.Select%2A> método de um <xref:Microsoft.Office.Interop.Word.Range> que contém o documento inteiro. O exemplo de código a seguir seleciona o conteúdo do documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>Para selecionar o documento inteiro como um intervalo usando a propriedade Content

1. Use a <xref:Microsoft.Office.Interop.Word._Document.Content%2A> propriedade para definir um intervalo que abrange todo o documento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet20":::

   Você também pode usar os métodos e as propriedades de outros objetos para definir um intervalo.

### <a name="to-select-a-sentence-in-the-active-document"></a>Para selecionar uma frase no documento ativo

1. Defina o intervalo usando a <xref:Microsoft.Office.Interop.Word.Sentences> coleção. Use o índice da frase que você deseja selecionar.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet21":::

   Outra maneira de selecionar uma sentença é definir manualmente os valores inicial e final para o intervalo.

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>Para selecionar uma sentença definindo manualmente os valores inicial e final

1. Crie uma variável de intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet23":::

2. Verifique se há pelo menos duas frases no documento, defina os argumentos de *início* e *término* do intervalo e, em seguida, selecione o intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet24":::

## <a name="see-also"></a>Consulte também
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como recuperar programaticamente caracteres de início e término em intervalos](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
