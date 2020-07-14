---
title: 'Como: Ocultar texto de forma programática em documentos'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4dae19d196f830e5187fa395473c0a5482cb1d03
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543306"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>Como: Ocultar texto de forma programática em documentos
  Você pode ocultar o texto em um documento definindo a <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Range.Font%2A> para um intervalo de texto específico.

 Por exemplo, você pode ocultar temporariamente o texto dentro de um <xref:Microsoft.Office.Tools.Word.Bookmark> (em uma personalização em nível de documento) ou um <xref:Microsoft.Office.Interop.Word.Bookmark> (em um suplemento do VSTO) antes de enviar um documento para uma impressora.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>Para ocultar o texto em um controle de indicador durante a impressão do documento

1. Crie um procedimento que oculta todo o texto que está em um intervalo especificado.

     [!code-vb[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#105)]
     [!code-csharp[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#105)]

2. Crie um procedimento que reexiba todo o texto que está em um intervalo especificado.

     [!code-vb[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#106)]
     [!code-csharp[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#106)]

3. Passe o intervalo de um indicador para o `HideText` método, imprima o documento e, em seguida, passe o mesmo intervalo para o `UnhideText` método.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento. Para usar este exemplo, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#107)]

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar o exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#107)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que o documento contém um <xref:Microsoft.Office.Tools.Word.Bookmark> controle (em uma personalização no nível do documento) ou <xref:Microsoft.Office.Interop.Word.Bookmark> controle (em um suplemento do VSTO) que é chamado `bookmark1` .

## <a name="see-also"></a>Confira também
- [Como: imprimir documentos programaticamente](../vsto/how-to-programmatically-print-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [Como: atualizar o texto do indicador programaticamente](../vsto/how-to-programmatically-update-bookmark-text.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
