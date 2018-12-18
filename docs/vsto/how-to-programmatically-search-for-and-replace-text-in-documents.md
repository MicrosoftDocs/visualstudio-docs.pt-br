---
title: 'Como: programaticamente, pesquisar e substituir texto em documentos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], searching
- text searches, replacing text
- text searches, documents
- text [Office development in Visual Studio], searching in documents
- text [Office development in Visual Studio], text searches
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6de96133a810898fe847cce71bb2711dd7c31dd9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822391"
---
# <a name="how-to-programmatically-search-for-and-replace-text-in-documents"></a>Como: programaticamente, pesquisar e substituir texto em documentos
  O <xref:Microsoft.Office.Interop.Word.Find> objeto é um membro de ambos os <xref:Microsoft.Office.Interop.Word.Selection> e o <xref:Microsoft.Office.Interop.Word.Range> objetos e você pode usar qualquer um para pesquisar texto em documentos do Microsoft Office Word. O comando Substituir é uma extensão do comando find.  
  
 Usar um <xref:Microsoft.Office.Interop.Word.Find> para executar um loop por meio de um documento do Microsoft Office Word e pesquisa de texto específico, a formatação ou o estilo do objeto e usar o <xref:Microsoft.Office.Interop.Word.Find.Replacement%2A> propriedade para substituir qualquer um dos itens encontrados.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="use-a-selection-object"></a>Usar um objeto de seleção  
 Quando você usa um <xref:Microsoft.Office.Interop.Word.Selection> objeto localizar texto, qualquer pesquisa critérios especificados por você são aplicados apenas em relação a no momento, o texto selecionado. Se o <xref:Microsoft.Office.Interop.Word.Selection> é um ponto de inserção, em seguida, o documento será pesquisado. Quando o item for encontrado que corresponde aos critérios de pesquisa, ele é selecionado automaticamente.  
  
 É importante observar que o <xref:Microsoft.Office.Interop.Word.Find> critérios são cumulativos, o que significa que os critérios são adicionados aos critérios de pesquisa anterior. Limpar formatação de pesquisas anteriores usando o <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> método antes da pesquisa.  
  
### <a name="to-find-text-using-a-selection-object"></a>Para localizar texto usando um objeto Selection  
  
1. Atribua uma cadeia de caracteres de pesquisa a uma variável.  
  
    [!code-vb[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#68)]
    [!code-csharp[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#68)]  
  
2. Limpe formatação de pesquisas anteriores.  
  
    [!code-vb[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#69)]
    [!code-csharp[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#69)]  
  
3. Executa a pesquisa e exibe uma caixa de mensagem com os resultados.  
  
    [!code-vb[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#70)]
    [!code-csharp[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#70)]  
  
   O exemplo a seguir mostra o método complete.  
  
   [!code-vb[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#67)]
   [!code-csharp[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#67)]  
  
## <a name="use-a-range-object"></a>Usar um objeto de intervalo  
 Usando um <xref:Microsoft.Office.Interop.Word.Range> objeto permite que você procure texto sem exibir qualquer coisa na interface do usuário. O <xref:Microsoft.Office.Interop.Word.Find> objeto retorna **verdadeira** se o texto for encontrado que corresponde aos critérios de pesquisa, e **False** se não existir. Ele também redefine o <xref:Microsoft.Office.Interop.Word.Range> objeto para corresponder aos critérios de pesquisa, se o texto for encontrado.  
  
### <a name="to-find-text-using-a-range-object"></a>Para localizar o texto usando um objeto de intervalo  
  
1. Definir um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste o segundo parágrafo no documento.  
  
    O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
    [!code-vb[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#72)]  
  
    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.  
  
    [!code-vb[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#72)]  
  
2. Usando o <xref:Microsoft.Office.Interop.Word.Range.Find%2A> propriedade do <xref:Microsoft.Office.Interop.Word.Range> do objeto, primeiro desmarque quaisquer opções de formatação existente e, em seguida, procure a cadeia de caracteres **estou me**.  
  
    [!code-vb[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#73)]
    [!code-csharp[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#73)]  
  
3. Exibir os resultados da pesquisa em uma caixa de mensagem e, em seguida, selecione o <xref:Microsoft.Office.Interop.Word.Range> para torná-la visível.  
  
    [!code-vb[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#74)]
    [!code-csharp[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#74)]  
  
    Se a pesquisa falhar, o segundo parágrafo está selecionado. Se tiver êxito, os critérios de pesquisa são exibidos.  
  
   O exemplo a seguir mostra o código completo para uma personalização no nível de documento. Para usar este exemplo, execute o código no `ThisDocument` classe em seu projeto.  
  
   [!code-vb[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#71)]  
  
   O exemplo a seguir mostra o código completo para um suplemento do VSTO. Para usar este exemplo, execute o código no `ThisAddIn` classe em seu projeto.  
  
   [!code-vb[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#71)]  
  
## <a name="search-for-and-replace-text-in-documents"></a>Pesquisar e substituir texto em documentos  
 O código a seguir pesquisa a seleção atual e substitui todas as ocorrências da cadeia de caracteres **estou me** com a cadeia de caracteres **encontrada**.  
  
### <a name="to-search-for-and-replace-text-in-documents"></a>Para pesquisar e substituir texto em documentos  
  
1.  Adicione o seguinte código de exemplo para o `ThisDocument` ou `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#75)]
     [!code-csharp[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#75)]  
  
     O <xref:Microsoft.Office.Interop.Word.Find> classe tem um <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> método e o <xref:Microsoft.Office.Interop.Word.Replacement> classe também tem seu próprio <xref:Microsoft.Office.Interop.Word.Replacement.ClearFormatting%2A> método. Quando você estiver executando operações de localizar e substituir, você deve usar o método ClearFormatting dos dois objetos. Se você usá-lo somente no <xref:Microsoft.Office.Interop.Word.Find> do objeto, você poderá obter resultados inesperados no texto de substituição.  
  
2.  Use o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método da <xref:Microsoft.Office.Interop.Word.Find> objeto a substituir cada item encontrado. Para especificar quais itens para substituir, use o *substituir* parâmetro. Esse parâmetro pode ser um dos seguintes <xref:Microsoft.Office.Interop.Word.WdReplace> valores:  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceAll> substitui todos os itens localizados.  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceNone> substitui a nenhum dos itens encontrados.  
  
    -   <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceOne> substitui o primeiro item encontrado.  
  
## <a name="see-also"></a>Consulte também  
 [Como: definir programaticamente as opções de pesquisa no Word](../vsto/how-to-programmatically-set-search-options-in-word.md)   
 [Como: executar um loop por meio de itens encontrados em documentos programaticamente](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  