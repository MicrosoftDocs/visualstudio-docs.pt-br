---
title: 'Como: executar um loop por meio de itens encontrados em documentos programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f36ddfa182d1a0440ca733b19c34a27b245007fc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49848053"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>Como: executar um loop por meio de itens encontrados em documentos programaticamente
  O <xref:Microsoft.Office.Interop.Word.Find> classe tem um <xref:Microsoft.Office.Interop.Word.Find.Found%2A> propriedade, que retorna **verdadeiro** sempre que um item pesquisado for encontrado. Você pode executar um loop por meio de todas as instâncias encontradas em uma <xref:Microsoft.Office.Interop.Word.Range> usando o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-loop-through-found-items"></a>Para percorrer itens encontrados  
  
1. Declarar uma <xref:Microsoft.Office.Interop.Word.Range> objeto.  
  
    O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
    [!code-vb[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#79)]  
  
    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.  
  
    [!code-vb[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#79)]  
  
2. Use o <xref:Microsoft.Office.Interop.Word.Find.Found%2A> propriedade em um loop para pesquisar todas as ocorrências da cadeia de caracteres no documento e incrementar uma variável de inteiro em 1 cada vez que a cadeia de caracteres for encontrada.  
  
    [!code-vb[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#80)]
    [!code-csharp[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#80)]  
  
3. Exiba o número de vezes que a cadeia de caracteres foi encontrada em uma caixa de mensagem.  
  
    [!code-vb[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#81)]
    [!code-csharp[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#81)]  
  
   Os exemplos a seguir mostram o método complete.  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização no nível de documento  
  
### <a name="to-loop-through-items-in-a-document-level-customization"></a>Para executar um loop por meio de itens em uma personalização no nível de documento  
  
1.  O exemplo a seguir mostra o código completo para uma personalização no nível de documento. Para usar esse código, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#78)]  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="to-loop-through-items-in-a-vsto-add-in"></a>Para executar um loop por meio de itens em um suplemento do VSTO  
  
1.  O exemplo a seguir mostra o código completo para um suplemento do VSTO. Para usar esse código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#78)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: pesquisar e substituir rext em documentos de forma programática](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)   
 [Como: definir programaticamente as opções de pesquisa no Word](../vsto/how-to-programmatically-set-search-options-in-word.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  