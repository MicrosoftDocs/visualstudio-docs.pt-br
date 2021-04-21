---
title: 'Como: inserir texto de forma programática em documentos do Word'
description: Saiba como você pode inserir texto de forma programática em um documento do Microsoft Word usando o Visual Studio.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f17828b4617f84cb104761918787b4bbb79f7afc
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827351"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>Como: inserir texto de forma programática em documentos do Word
  Há três maneiras principais de inserir texto em Microsoft Office documentos do Word:

- Inserir texto em um intervalo.

- Substituir o texto em um intervalo por um novo texto.

- Use o <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> método de um <xref:Microsoft.Office.Interop.Word.Selection> objeto para inserir texto no cursor ou na seleção.

> [!NOTE]
> Você também pode inserir texto em controles de conteúdo e indicadores. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md) e controle de [indicador](../vsto/bookmark-control.md).

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="insert-text-in-a-range"></a>Inserir texto em um intervalo
 Use a <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade de um <xref:Microsoft.Office.Interop.Word.Range> objeto para inserir texto em um documento.

### <a name="to-insert-text-in-a-range"></a>Para inserir texto em um intervalo

1. Especifique um intervalo no início de um documento e insira o texto **novo texto**.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet51":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet51":::

2. Selecione o <xref:Microsoft.Office.Interop.Word.Range> objeto, que foi expandido de um caractere para o comprimento do texto inserido.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet52":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet52":::

## <a name="replace-text-in-a-range"></a>Substituir texto em um intervalo
 Se o intervalo especificado contiver texto, todo o texto no intervalo será substituído pelo texto inserido.

### <a name="to-replace-text-in-a-range"></a>Para substituir o texto em um intervalo

1. Crie um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste nos primeiros 12 caracteres no documento.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet53":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet53":::

2. Substitua esses caracteres pelo **novo texto** da cadeia de caracteres.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet54":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet54":::

3. Selecione o intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet55":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet55":::

## <a name="insert-text-using-typetext"></a>Inserir texto usando TypeText
 O <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> método insere texto na seleção. <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> comporta-se de forma diferente dependendo das opções definidas no computador do usuário. O código no procedimento a seguir declara uma <xref:Microsoft.Office.Interop.Word.Selection> variável de objeto e desativa a opção **sobrescrever** se ela estiver ativada. Se a opção **sobrescrever** estiver ativada, qualquer texto ao lado do cursor será substituído.

### <a name="to-insert-text-using-the-typetext-method"></a>Para inserir texto usando o método TypeText

1. Declare uma variável do objeto <xref:Microsoft.Office.Interop.Word.Selection>.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet57":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet57":::

2. Desative a opção **sobrescrever** se ela estiver ativada.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet58":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet58":::

3. Teste para ver se a seleção atual é um ponto de inserção.

    Se for, o código inserirá uma frase usando <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> e, em seguida, uma marca de parágrafo usando o <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> método.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet59":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet59":::

4. O código no bloco **ElseIf** testa para ver se a seleção é uma seleção normal. Se for, outro **se** bloquear testes para ver se a opção **ReplaceSelection** está ativada. Se for, o código usará o <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> método da seleção para recolher a seleção para um ponto de inserção no início do bloco de texto selecionado. Insira o texto e uma marca de parágrafo.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet60":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet60":::

5. Se a seleção não for um ponto de inserção ou um bloco de texto selecionado, o código no bloco **else** não fará nada.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet61":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet61":::

   Você também pode usar o <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> método do <xref:Microsoft.Office.Interop.Word.Selection> objeto, que imita a funcionalidade da tecla **Backspace** no teclado. No entanto, quando se trata de inserir e manipular texto, o <xref:Microsoft.Office.Interop.Word.Range> objeto oferece a você mais controle.

   O exemplo a seguir mostra todo o código. Para usar este exemplo, execute o código da `ThisDocument` classe ou `ThisAddIn` em seu projeto.

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet56":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet56":::

## <a name="see-also"></a>Consulte também
- [Como: formatar texto de forma programática em documentos](../vsto/how-to-programmatically-format-text-in-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
