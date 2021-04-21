---
title: Excluir marcas de parágrafo ao criar intervalos programaticamente
description: Saiba como você pode excluir de forma programática marcas de parágrafo ao criar intervalos em um documento do Microsoft Word.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], excluding paragraphs
- ranges, excluding paragraph marks in Word
- documents [Office development in Visual Studio], paragraph marks
- paragraphs, controlling structure
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c0929ccf3bb2567099dc7f3b795ad2257da0edb3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825791"
---
# <a name="how-to-programmatically-exclude-paragraph-marks-when-creating-ranges"></a>Como: excluir programaticamente marcas de parágrafo ao criar intervalos
  Sempre que você cria um <xref:Microsoft.Office.Interop.Word.Range> objeto com base em um parágrafo, todos os caracteres não imprimíveis, como marcas de parágrafo, são incluídos no intervalo. Talvez você queira inserir o texto de um parágrafo de origem em um parágrafo de destino. Se você não quiser dividir o parágrafo de destino em parágrafos separados, primeiro deverá remover a marca de parágrafo do parágrafo de origem. Além disso, como as informações de formatação de parágrafo são armazenadas na marca de parágrafo, talvez você não queira incluí-las ao inserir o intervalo em um parágrafo existente.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 O procedimento de exemplo a seguir declara duas variáveis de cadeia de caracteres, recupera o conteúdo do primeiro e do segundo parágrafo no documento ativo e, em seguida, troca seu conteúdo. Em seguida, o exemplo demonstra a remoção do marcador de parágrafo do intervalo usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método e a inserção de texto dentro do parágrafo.

## <a name="to-control-paragraph-structure-when-inserting-text"></a>Para controlar a estrutura do parágrafo ao inserir texto

1. Crie duas variáveis de intervalo para o primeiro e o segundo parágrafos e recupere seu conteúdo usando a <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet27":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet27":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO em nível de aplicativo. Esse código usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet27":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet27":::

2. Atribua a <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade, trocando o texto entre os dois parágrafos.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet28":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet28":::

3. Selecione cada intervalo por vez e Pause para exibir os resultados em uma caixa de mensagem.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet29":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet29":::

4. Ajuste `firstRange` usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método para que o marcador de parágrafo não faça mais parte do `firstRange` .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet30":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet30":::

5. Substitua o restante do texto no primeiro parágrafo, atribuindo uma nova cadeia de caracteres à <xref:Microsoft.Office.Interop.Word.Range.Text%2A> Propriedade do intervalo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet31":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet31":::

6. Substitua o texto em `secondRange` , incluindo a marca de parágrafo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet32":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet32":::

7. Selecione `firstRange` e Pause para exibir os resultados em uma caixa de mensagem e, em seguida, faça o mesmo com `secondRange` .

     Como `firstRange` o foi redefinido para excluir a marca de parágrafo, a formatação original do parágrafo é preservada. No entanto, uma sentença foi inserida na marca de parágrafo `secondRange` , removendo o parágrafo separado.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet33":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet33":::

     O conteúdo original de ambos os intervalos foi salvo como cadeias de caracteres, portanto, você pode restaurar o documento para sua condição original.

8. Reajuste `firstRange` para incluir a marca de parágrafo usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método para a posição de um caractere.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet34":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet34":::

9. Excluir `secondRange`. Isso restaura o parágrafo três para sua posição original.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet35":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet35":::

10. Restaurar o texto do parágrafo original em `firstRange` .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet36":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet36":::

11. Use o <xref:Microsoft.Office.Interop.Word.Range.InsertAfter%2A> método do <xref:Microsoft.Office.Interop.Word.Range> objeto para inserir o parágrafo original-dois conteúdos após `firstRange` e, em seguida, selecione `firstRange` .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet37":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet37":::

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-control-paragraph-structure-when-inserting-text-in-document-level-customizations"></a>Para controlar a estrutura do parágrafo ao inserir texto em personalizações em nível de documento

1. O exemplo a seguir mostra o método completo para uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet26":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet26":::

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-control-paragraph-structure-when-inserting-text-in-a-vsto-add-in"></a>Para controlar a estrutura do parágrafo ao inserir texto em um suplemento do VSTO

1. O exemplo a seguir mostra o método completo para um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet26":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet26":::

## <a name="see-also"></a>Consulte também
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
