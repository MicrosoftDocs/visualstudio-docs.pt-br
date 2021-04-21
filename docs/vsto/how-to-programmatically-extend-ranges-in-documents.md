---
title: 'Como: estender intervalos programaticamente em documentos'
description: Saiba como você pode estender programaticamente intervalos de pontos de início e de término em um documento do Microsoft Word no nível do documento ou do aplicativo.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, extending
- documents [Office development in Visual Studio], extending ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7a539bbbc4ad8d73477e660ef9903ac51dce712f
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826519"
---
# <a name="how-to-programmatically-extend-ranges-in-documents"></a>Como: estender intervalos programaticamente em documentos
  Depois de definir um <xref:Microsoft.Office.Interop.Word.Range> objeto em um Microsoft Office documento do Word, você altera seus pontos inicial e final usando os <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> métodos e. Os <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> métodos e usam os mesmos dois argumentos, *unidade* e *contagem*. O argumento *Count* é o número de unidades a serem movidas e o argumento *Unit* pode ser um dos seguintes <xref:Microsoft.Office.Interop.Word.WdUnits> valores:

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCharacter>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdWord>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSentence>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdParagraph>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSection>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdStory>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCell>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdColumn>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdRow>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdTable>

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

  O exemplo a seguir define um intervalo de sete caracteres. Em seguida, ele move a posição inicial do intervalo de sete caracteres após a posição inicial original. Como a posição final do intervalo também tinha sete caracteres após a posição inicial, o resultado é um intervalo que consiste em zero caracteres. Em seguida, o código move a posição final sete caracteres após a posição final atual.

## <a name="to-extend-a-range"></a>Para estender um intervalo

1. Defina um intervalo de caracteres. Para obter mais informações, consulte [como: definir e selecionar intervalos por meio de programação em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md).

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet39":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet39":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet39":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet39":::

2. Use o <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> método do <xref:Microsoft.Office.Interop.Word.Range> objeto para mover a posição inicial do intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet40":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet40":::

3. Use o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método do <xref:Microsoft.Office.Interop.Word.Range> objeto para mover a posição final do intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet41":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet41":::

## <a name="document-level-customization-code"></a>Código de personalização no nível do documento

### <a name="to-extend-a-range-in-a-document-level-customization"></a>Para estender um intervalo em uma personalização no nível do documento

1. O exemplo a seguir mostra o código completo de uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet38":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet38":::

## <a name="vsto-add-in-code"></a>Código do suplemento do VSTO

### <a name="to-extend-a-range-in-an-application-level-vsto-add-in"></a>Para estender um intervalo em um suplemento do VSTO em nível de aplicativo

1. O exemplo a seguir mostra o código completo de um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet38":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet38":::

## <a name="see-also"></a>Consulte também
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como recuperar programaticamente caracteres de início e término em intervalos](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
