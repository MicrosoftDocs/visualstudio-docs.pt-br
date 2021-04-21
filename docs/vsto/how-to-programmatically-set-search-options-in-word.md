---
title: 'Como: definir opções de pesquisa de forma programática no Word'
description: Saiba como você pode usar o Visual Studio para definir opções de pesquisa para seleções no Microsoft Word de forma programática.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 605f782bf6dc3bb56b52bdcd896d1c6419cf5f51
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825024"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>Como: definir opções de pesquisa de forma programática no Word
  Há duas maneiras de definir opções de pesquisa para seleções em documentos Microsoft Office Word:

- Defina as propriedades individuais de um <xref:Microsoft.Office.Interop.Word.Find> objeto.

- Use argumentos do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto.

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>Usar propriedades de um objeto Find
 O código a seguir define as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para Pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como Pesquisar em frente, disposição e texto a serem pesquisados, são propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto.

 A definição de cada uma das propriedades do <xref:Microsoft.Office.Interop.Word.Find> objeto não é útil quando você escreve o código C#, pois você deve especificar as mesmas propriedades como parâmetros no <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método. Portanto, este exemplo contém apenas Visual Basic código.

### <a name="to-set-search-options-using-a-find-object"></a>Para definir as opções de pesquisa usando um objeto Find

1. Defina as propriedades de um <xref:Microsoft.Office.Interop.Word.Find> objeto para pesquisar adiante por uma seleção para o texto **encontrá-** lo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet76":::

## <a name="use-execute-method-arguments"></a>Usar argumentos do método execute
 O código a seguir usa o <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método de um <xref:Microsoft.Office.Interop.Word.Find> objeto para Pesquisar texto dentro da seleção atual. Observe que os critérios de pesquisa, como Pesquisar em frente, disposição e texto a serem pesquisados, são passados como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método.

### <a name="to-set-search-options-using-execute-method-arguments"></a>Para definir as opções de pesquisa usando argumentos de método execute

1. Passe os critérios de pesquisa como parâmetros do <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método para pesquisar em uma seleção para o texto **encontrá-** lo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet77":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet77":::

## <a name="see-also"></a>Consulte também
- [Como: Pesquisar e substituir texto de forma programática em documentos](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [Como fazer loops programaticamente por meio de itens encontrados em documentos](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)
