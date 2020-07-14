---
title: Excluir marcas de parágrafo ao criar intervalos programaticamente
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 20d91aff6b09e659375494c387eea94ef05cc682
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547427"
---
# <a name="how-to-programmatically-exclude-paragraph-marks-when-creating-ranges"></a>Como: excluir programaticamente marcas de parágrafo ao criar intervalos
  Sempre que você cria um <xref:Microsoft.Office.Interop.Word.Range> objeto com base em um parágrafo, todos os caracteres não imprimíveis, como marcas de parágrafo, são incluídos no intervalo. Talvez você queira inserir o texto de um parágrafo de origem em um parágrafo de destino. Se você não quiser dividir o parágrafo de destino em parágrafos separados, primeiro deverá remover a marca de parágrafo do parágrafo de origem. Além disso, como as informações de formatação de parágrafo são armazenadas na marca de parágrafo, talvez você não queira incluí-las ao inserir o intervalo em um parágrafo existente.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 O procedimento de exemplo a seguir declara duas variáveis de cadeia de caracteres, recupera o conteúdo do primeiro e do segundo parágrafo no documento ativo e, em seguida, troca seu conteúdo. Em seguida, o exemplo demonstra a remoção do marcador de parágrafo do intervalo usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método e a inserção de texto dentro do parágrafo.

## <a name="to-control-paragraph-structure-when-inserting-text"></a>Para controlar a estrutura do parágrafo ao inserir texto

1. Crie duas variáveis de intervalo para o primeiro e o segundo parágrafos e recupere seu conteúdo usando a <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     [!code-vb[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#27)]

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO em nível de aplicativo. Esse código usa o documento ativo.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#27)]

2. Atribua a <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade, trocando o texto entre os dois parágrafos.

     [!code-vb[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#28)]
     [!code-csharp[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#28)]

3. Selecione cada intervalo por vez e Pause para exibir os resultados em uma caixa de mensagem.

     [!code-vb[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#29)]
     [!code-csharp[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#29)]

4. Ajuste `firstRange` usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método para que o marcador de parágrafo não faça mais parte do `firstRange` .

     [!code-vb[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#30)]
     [!code-csharp[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#30)]

5. Substitua o restante do texto no primeiro parágrafo, atribuindo uma nova cadeia de caracteres à <xref:Microsoft.Office.Interop.Word.Range.Text%2A> Propriedade do intervalo.

     [!code-vb[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#31)]
     [!code-csharp[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#31)]

6. Substitua o texto em `secondRange` , incluindo a marca de parágrafo.

     [!code-vb[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#32)]
     [!code-csharp[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#32)]

7. Selecione `firstRange` e Pause para exibir os resultados em uma caixa de mensagem e, em seguida, faça o mesmo com `secondRange` .

     Como `firstRange` o foi redefinido para excluir a marca de parágrafo, a formatação original do parágrafo é preservada. No entanto, uma sentença foi inserida na marca de parágrafo `secondRange` , removendo o parágrafo separado.

     [!code-vb[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#33)]
     [!code-csharp[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#33)]

     O conteúdo original de ambos os intervalos foi salvo como cadeias de caracteres, portanto, você pode restaurar o documento para sua condição original.

8. Reajuste `firstRange` para incluir a marca de parágrafo usando o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método para a posição de um caractere.

     [!code-vb[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#34)]
     [!code-csharp[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#34)]

9. Excluir `secondRange`. Isso restaura o parágrafo três para sua posição original.

     [!code-vb[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#35)]
     [!code-csharp[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#35)]

10. Restaurar o texto do parágrafo original em `firstRange` .

     [!code-vb[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#36)]
     [!code-csharp[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#36)]

11. Use o <xref:Microsoft.Office.Interop.Word.Range.InsertAfter%2A> método do <xref:Microsoft.Office.Interop.Word.Range> objeto para inserir o parágrafo original-dois conteúdos após `firstRange` e, em seguida, selecione `firstRange` .

     [!code-vb[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#37)]
     [!code-csharp[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#37)]

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-control-paragraph-structure-when-inserting-text-in-document-level-customizations"></a>Para controlar a estrutura do parágrafo ao inserir texto em personalizações em nível de documento

1. O exemplo a seguir mostra o método completo para uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#26)]

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-control-paragraph-structure-when-inserting-text-in-a-vsto-add-in"></a>Para controlar a estrutura do parágrafo ao inserir texto em um suplemento do VSTO

1. O exemplo a seguir mostra o método completo para um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#26)]

## <a name="see-also"></a>Confira também
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
