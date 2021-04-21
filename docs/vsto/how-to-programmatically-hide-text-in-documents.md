---
title: 'Como: Ocultar texto de forma programática em documentos'
description: Saiba como você pode ocultar texto em um documento do Microsoft Word definindo a Propriedade Hidden da fonte para um intervalo de texto específico.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 04ea6b56519656782a3e408892235fa177eef755
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826480"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>Como: Ocultar texto de forma programática em documentos
  Você pode ocultar o texto em um documento definindo a <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Range.Font%2A> para um intervalo de texto específico.

 Por exemplo, você pode ocultar temporariamente o texto dentro de um <xref:Microsoft.Office.Tools.Word.Bookmark> (em uma personalização em nível de documento) ou um <xref:Microsoft.Office.Interop.Word.Bookmark> (em um suplemento do VSTO) antes de enviar um documento para uma impressora.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>Para ocultar o texto em um controle de indicador durante a impressão do documento

1. Crie um procedimento que oculta todo o texto que está em um intervalo especificado.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet105":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet105":::

2. Crie um procedimento que reexiba todo o texto que está em um intervalo especificado.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet106":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet106":::

3. Passe o intervalo de um indicador para o `HideText` método, imprima o documento e, em seguida, passe o mesmo intervalo para o `UnhideText` método.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento. Para usar este exemplo, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet107":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet107":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar o exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet107":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet107":::

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que o documento contém um <xref:Microsoft.Office.Tools.Word.Bookmark> controle (em uma personalização no nível do documento) ou <xref:Microsoft.Office.Interop.Word.Bookmark> controle (em um suplemento do VSTO) que é chamado `bookmark1` .

## <a name="see-also"></a>Consulte também
- [Como: imprimir documentos programaticamente](../vsto/how-to-programmatically-print-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: atualizar o texto do indicador programaticamente](../vsto/how-to-programmatically-update-bookmark-text.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
