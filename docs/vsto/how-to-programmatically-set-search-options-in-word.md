---
title: 'Como: Definir programaticamente as opções de pesquisa no Word'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6e3b66bfd7f3f5d0ef0f4893efeb81c80df5d4ae
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60093508"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>Como: Definir programaticamente as opções de pesquisa no Word
  Há duas maneiras de definir opções de pesquisa para seleções em documentos do Microsoft Office Word:

- Definir propriedades individuais de um <xref:Microsoft.Office.Interop.Word.Find> objeto.

- Usar argumentos do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto.

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>Usar propriedades de um objeto de localização
 O código a seguir define as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como a pesquisa de encaminhamento, encapsulamento e texto a ser pesquisado, são propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto.

 Definindo cada uma das propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto não é útil quando você escreve código em c# porque você deve especificar as mesmas propriedades como parâmetros no <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método. Portanto, este exemplo contém apenas código do Visual Basic.

### <a name="to-set-search-options-using-a-find-object"></a>Para definir opções de pesquisa usando um objeto Find

1. Definir as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar adiante por meio de uma seleção para o texto **estou me**.

     [!code-vb[Trin_VstcoreWordAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#76)]

## <a name="use-execute-method-arguments"></a>Usar argumentos de método Execute
 O código a seguir usa o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como a pesquisa de encaminhamento, encapsulamento e texto a ser pesquisado, são passados como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método.

### <a name="to-set-search-options-using-execute-method-arguments"></a>Para definir opções de pesquisa usando os argumentos de método Execute

1. Passe critérios de pesquisa como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método para pesquisar adiante por meio de uma seleção para o texto **estou me**.

     [!code-vb[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#77)]
     [!code-csharp[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#77)]

## <a name="see-also"></a>Consulte também
- [Como: Programaticamente, pesquisar e substituir texto em documentos](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [Como: Executar um loop por meio de itens encontrados em documentos programaticamente](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Como: Por meio de programação restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)
