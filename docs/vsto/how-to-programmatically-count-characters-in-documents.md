---
title: 'Como: contar caracteres programaticamente em documentos'
description: Saiba como você pode determinar o número de caracteres em um documento usando a propriedade Count da coleção de caracteres.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- characters, counting in documents
- counting characters in documents
- documents [Office development in Visual Studio], counting characters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 68ddc86183eacd7f76e39bb06e47968c0129849c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823997"
---
# <a name="how-to-programmatically-count-characters-in-documents"></a>Como: contar caracteres programaticamente em documentos
  O primeiro caractere em um documento está na posição do caractere 0, que representa o ponto de inserção. A última posição de caractere é igual ao número total de caracteres no documento. Você pode determinar o número de caracteres em um documento usando a <xref:Microsoft.Office.Interop.Word.Characters.Count%2A> propriedade da <xref:Microsoft.Office.Interop.Word.Characters> coleção.

 Todos os caracteres no documento são contados, incluindo espaços, marcas de parágrafo e outros caracteres que normalmente são ocultos. Mesmo um novo documento em branco retorna uma contagem de um caractere, pois ele contém uma marca de parágrafo.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-display-the-number-of-characters-in-a-document-level-customization"></a>Para exibir o número de caracteres em uma personalização em nível de documento

1. Selecione o documento inteiro.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet98":::

2. Exibe o número de caracteres no documento em uma caixa de mensagem.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet99":::

## <a name="to-display-the-number-of-characters-in-a-vsto-add-in"></a>Para exibir o número de caracteres em um suplemento do VSTO

1. Selecione o documento inteiro. O exemplo a seguir seleciona o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet98":::

2. Exibe o número de caracteres no documento em uma caixa de mensagem.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet99":::

## <a name="see-also"></a>Consulte também
- [Como recuperar programaticamente caracteres de início e término em intervalos](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
