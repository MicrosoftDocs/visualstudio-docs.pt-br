---
title: 'Como: definir programaticamente as opções de pesquisa no Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4e4e6b5471f1d36eab677d8a1d0b65ab39b7dba4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853930"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>Como: definir programaticamente as opções de pesquisa no Word
  Há duas maneiras de definir opções de pesquisa para seleções em documentos do Microsoft Office Word:  
  
- Definir propriedades individuais de um <xref:Microsoft.Office.Interop.Word.Find> objeto.  
  
- Usar argumentos do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto.  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="use-properties-of-a-find-object"></a>Usar propriedades de um objeto de localização  
 O código a seguir define as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como a pesquisa de encaminhamento, encapsulamento e texto a ser pesquisado, são propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto.  
  
 Definindo cada uma das propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto não é útil quando você escreve código em c# porque você deve especificar as mesmas propriedades como parâmetros no <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método. Portanto, este exemplo contém apenas código do Visual Basic.  
  
### <a name="to-set-search-options-using-a-find-object"></a>Para definir opções de pesquisa usando um objeto Find  
  
1.  Definir as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar adiante por meio de uma seleção para o texto **estou me**.  
  
     [!code-vb[Trin_VstcoreWordAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#76)]  
  
## <a name="use-execute-method-arguments"></a>Usar argumentos de método Execute  
 O código a seguir usa o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como a pesquisa de encaminhamento, encapsulamento e texto a ser pesquisado, são passados como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método.  
  
### <a name="to-set-search-options-using-execute-method-arguments"></a>Para definir opções de pesquisa usando os argumentos de método Execute  
  
1.  Passe critérios de pesquisa como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método para pesquisar adiante por meio de uma seleção para o texto **estou me**.  
  
     [!code-vb[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#77)]
     [!code-csharp[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#77)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: programaticamente, pesquisar e substituir texto em documentos](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)   
 [Como: executar um loop por meio de itens encontrados em documentos programaticamente](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)   
 [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)  
  
  