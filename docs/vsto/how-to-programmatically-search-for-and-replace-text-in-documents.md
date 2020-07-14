---
title: Localizar e substituir texto em documentos programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], searching
- text searches, replacing text
- text searches, documents
- text [Office development in Visual Studio], searching in documents
- text [Office development in Visual Studio], text searches
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 18a50d6d4ef52a0c50be0b72b4cab5706da4e2db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547037"
---
# <a name="how-to-programmatically-search-for-and-replace-text-in-documents"></a>Como: Pesquisar e substituir texto de forma programática em documentos
  O <xref:Microsoft.Office.Interop.Word.Find> objeto é um membro dos <xref:Microsoft.Office.Interop.Word.Selection> objetos e e <xref:Microsoft.Office.Interop.Word.Range> você pode usar qualquer um para pesquisar texto em Microsoft Office documentos do Word. O comando Replace é uma extensão do comando find.

 Use um <xref:Microsoft.Office.Interop.Word.Find> objeto para executar um loop em um Microsoft Office documento do Word e Pesquisar texto, formatação ou estilo específicos e usar a <xref:Microsoft.Office.Interop.Word.Find.Replacement%2A> propriedade para substituir qualquer um dos itens encontrados.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-a-selection-object"></a>Usar um objeto de seleção
 Quando você usa um <xref:Microsoft.Office.Interop.Word.Selection> objeto para localizar texto, os critérios de pesquisa especificados são aplicados somente no texto atualmente selecionado. Se <xref:Microsoft.Office.Interop.Word.Selection> for um ponto de inserção, o documento será pesquisado. Quando o item que corresponde aos critérios de pesquisa é encontrado, ele é selecionado automaticamente.

 É importante observar que os <xref:Microsoft.Office.Interop.Word.Find> critérios são cumulativos, o que significa que os critérios são adicionados aos critérios de pesquisa anteriores. Limpar a formatação de pesquisas anteriores usando o <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> método anterior à pesquisa.

### <a name="to-find-text-using-a-selection-object"></a>Para localizar texto usando um objeto de seleção

1. Atribua uma cadeia de caracteres de pesquisa a uma variável.

    [!code-vb[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#68)]
    [!code-csharp[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#68)]

2. Limpar formatação de pesquisas anteriores.

    [!code-vb[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#69)]
    [!code-csharp[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#69)]

3. Execute a pesquisa e exiba uma caixa de mensagem com os resultados.

    [!code-vb[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#70)]
    [!code-csharp[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#70)]

   O exemplo a seguir mostra o método Complete.

   [!code-vb[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#67)]
   [!code-csharp[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#67)]

## <a name="use-a-range-object"></a>Usar um objeto Range
 O uso de um <xref:Microsoft.Office.Interop.Word.Range> objeto permite Pesquisar texto sem exibir nada na interface do usuário. O <xref:Microsoft.Office.Interop.Word.Find> objeto retornará **true** se for encontrado texto que corresponde aos critérios de pesquisa e **false** se não. Ele também redefine o <xref:Microsoft.Office.Interop.Word.Range> objeto para corresponder aos critérios de pesquisa se o texto for encontrado.

### <a name="to-find-text-using-a-range-object"></a>Para localizar texto usando um objeto Range

1. Defina um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste no segundo parágrafo do documento.

    O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

    [!code-vb[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#72)]

    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#72)]

2. Usando a <xref:Microsoft.Office.Interop.Word.Range.Find%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Range> objeto, primeiro desmarque todas as opções de formatação existentes e, em seguida, procure a cadeia de caracteres **Localize-me**.

    [!code-vb[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#73)]
    [!code-csharp[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#73)]

3. Exiba os resultados da pesquisa em uma caixa de mensagem e selecione o <xref:Microsoft.Office.Interop.Word.Range> para torná-lo visível.

    [!code-vb[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#74)]
    [!code-csharp[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#74)]

    Se a pesquisa falhar, o segundo parágrafo será selecionado; Se tiver sucesso, os critérios de pesquisa serão exibidos.

   O exemplo a seguir mostra o código completo de uma personalização em nível de documento. Para usar este exemplo, execute o código da `ThisDocument` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#71)]

   O exemplo a seguir mostra o código completo de um suplemento do VSTO. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#71)]

## <a name="search-for-and-replace-text-in-documents"></a>Pesquisar e substituir texto em documentos
 O código a seguir pesquisa a seleção atual e substitui todas as ocorrências da cadeia de caracteres, **encontre-me** com a cadeia de caracteres **encontrada**.

### <a name="to-search-for-and-replace-text-in-documents"></a>Para pesquisar e substituir texto em documentos

1. Adicione o seguinte código de exemplo à `ThisDocument` `ThisAddIn` classe ou em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#75)]
     [!code-csharp[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#75)]

     A <xref:Microsoft.Office.Interop.Word.Find> classe tem um <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> método e a <xref:Microsoft.Office.Interop.Word.Replacement> classe também tem seu próprio <xref:Microsoft.Office.Interop.Word.Replacement.ClearFormatting%2A> método. Ao executar operações de localizar e substituir, você deve usar o método ClearFormatting de ambos os objetos. Se você usá-lo somente no <xref:Microsoft.Office.Interop.Word.Find> objeto, poderá obter resultados imprevistos no texto de substituição.

2. Use o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método do <xref:Microsoft.Office.Interop.Word.Find> objeto para substituir cada item encontrado. Para especificar quais itens substituir, use o parâmetro *replace* . Esse parâmetro pode ser um dos seguintes <xref:Microsoft.Office.Interop.Word.WdReplace> valores:

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceAll>substitui todos os itens encontrados.

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceNone>Substitui nenhum dos itens encontrados.

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceOne>Substitui o primeiro item encontrado.

## <a name="see-also"></a>Confira também
- [Como: definir opções de pesquisa de forma programática no Word](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [Como fazer loops programaticamente por meio de itens encontrados em documentos](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
