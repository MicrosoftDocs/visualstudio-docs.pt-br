---
title: 'Como: formatar texto de forma programática em documentos'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- documents [Office development in Visual Studio], formatting text
- text [Office development in Visual Studio], formatting in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76af290b0e32126689dbe7b60f27889d9742ea7f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519841"
---
# <a name="how-to-programmatically-format-text-in-documents"></a>Como: formatar texto de forma programática em documentos
  Você pode usar o <xref:Microsoft.Office.Interop.Word.Range> objeto para formatar texto em um Microsoft Office documento do Word.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 O exemplo a seguir seleciona o primeiro parágrafo no documento e altera o tamanho da fonte, o nome da fonte e o alinhamento. Em seguida, ele seleciona o intervalo e exibe uma caixa de mensagem para pausar antes de executar a próxima seção do código. A próxima seção chama o método Undo do <xref:Microsoft.Office.Tools.Word.Document> item de host (para uma personalização em nível de documento) ou a <xref:Microsoft.Office.Interop.Word.Document> classe (para um suplemento do VSTO) três vezes. Ele aplica o estilo de recuo normal e exibe uma caixa de mensagem para pausar o código. Em seguida, o código chama o <xref:Microsoft.Office.Tools.Word.Document.Undo%2A> método uma vez e exibe uma caixa de mensagem.

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-format-text-using-a-document-level-customization"></a>Para formatar o texto usando uma personalização no nível do documento

1. O exemplo a seguir pode ser usado em uma personalização no nível do documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#62)]

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-format-text-using-a-vsto-add-in"></a>Para formatar o texto usando um suplemento do VSTO

1. O exemplo a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#62)]

## <a name="see-also"></a>Confira também
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Como: Pesquisar e substituir texto de forma programática em documentos](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
