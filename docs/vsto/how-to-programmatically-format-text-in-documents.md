---
title: 'Como: Formatar o texto em documentos programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- documents [Office development in Visual Studio], formatting text
- text [Office development in Visual Studio], formatting in documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: baf6f49b0347aa4a770b4f7a47c7fa8195d5ede5
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257404"
---
# <a name="how-to-programmatically-format-text-in-documents"></a>Como: Formatar o texto em documentos programaticamente
  Você pode usar o <xref:Microsoft.Office.Interop.Word.Range> objeto para formatar o texto em um documento do Microsoft Office Word.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 O exemplo a seguir seleciona o primeiro parágrafo no documento e altera o tamanho da fonte, o nome da fonte e o alinhamento. Em seguida, ele seleciona o intervalo e exibe uma caixa de mensagem para pausar antes de executar a próxima seção de código. A próxima seção chama o método Undo do <xref:Microsoft.Office.Tools.Word.Document> item de host (para uma personalização no nível de documento) ou o <xref:Microsoft.Office.Interop.Word.Document> classe (para um suplemento VSTO) três vezes. Ele aplica o estilo do recuo Normal e exibe uma caixa de mensagem para pausar o código. Em seguida, o código chama o <xref:Microsoft.Office.Tools.Word.Document.Undo%2A> método uma vez e exibe uma caixa de mensagem.  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização no nível de documento  
  
### <a name="to-format-text-using-a-document-level-customization"></a>Para formatar o texto usando uma personalização no nível de documento  
  
1.  O exemplo a seguir pode ser usado em uma personalização no nível de documento. Para usar esse código, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#62)]  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="to-format-text-using-a-vsto-add-in"></a>Para formatar o texto usando um suplemento do VSTO  
  
1.  O exemplo a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar esse código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#62)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: programaticamente, inserir texto em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)   
 [Como: programaticamente, pesquisar e substituir texto em documentos](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)  
  
  