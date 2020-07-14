---
title: Como fazer loops programaticamente por meio de itens encontrados em documentos
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e200f910e002bb9380bd5a1b556dc6f1cab08810
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544736"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>Como fazer loops programaticamente por meio de itens encontrados em documentos
  A <xref:Microsoft.Office.Interop.Word.Find> classe tem uma <xref:Microsoft.Office.Interop.Word.Find.Found%2A> propriedade, que retorna **true** sempre que um item procurado for encontrado. Você pode executar um loop em todas as instâncias encontradas em um <xref:Microsoft.Office.Interop.Word.Range> usando o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-loop-through-found-items"></a>Para executar um loop nos itens encontrados

1. Declare um <xref:Microsoft.Office.Interop.Word.Range> objeto.

    O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

    [!code-vb[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#79)]

    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#79)]

2. Use a <xref:Microsoft.Office.Interop.Word.Find.Found%2A> propriedade em um loop para pesquisar todas as ocorrências da cadeia de caracteres no documento e incrementar uma variável de inteiro em 1 cada vez que a cadeia de caracteres for encontrada.

    [!code-vb[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#80)]
    [!code-csharp[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#80)]

3. Exibe o número de vezes que a cadeia de caracteres foi encontrada em uma caixa de mensagem.

    [!code-vb[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#81)]
    [!code-csharp[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#81)]

   Os exemplos a seguir mostram o método Complete.

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-loop-through-items-in-a-document-level-customization"></a>Para executar um loop por meio de itens em uma personalização no nível do documento

1. O exemplo a seguir mostra o código completo de uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#78)]

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>Para executar um loop por meio de itens em um suplemento do VSTO

1. O exemplo a seguir mostra o código completo de um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#78)]

## <a name="see-also"></a>Consulte também
- [Como: Pesquisar e substituir rext em documentos de forma programática](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [Como: definir opções de pesquisa de forma programática no Word](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
