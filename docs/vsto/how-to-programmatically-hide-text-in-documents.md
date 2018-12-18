---
title: 'Como: ocultar texto em documentos de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 83b25c37ee2ce4dd9cb1ffeda21fbda1b5f3f139
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670232"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>Como: ocultar texto em documentos de forma programática
  Você pode ocultar texto em um documento Configurando o <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> propriedade do <xref:Microsoft.Office.Interop.Word.Range.Font%2A> para um determinado intervalo de texto.  
  
 Por exemplo, você pode ocultar temporariamente o texto dentro de um <xref:Microsoft.Office.Tools.Word.Bookmark> (em uma personalização no nível de documento) ou um <xref:Microsoft.Office.Interop.Word.Bookmark> (em um suplemento VSTO) antes de enviar um documento para uma impressora.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>Para ocultar texto em um controle de indicador ao imprimir o documento  
  
1.  Crie um procedimento que oculta todo o texto que está em um intervalo especificado.  
  
     [!code-vb[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#105)]
     [!code-csharp[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#105)]  
  
2.  Crie um procedimento que exibe novamente todo o texto que está em um intervalo especificado.  
  
     [!code-vb[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#106)]
     [!code-csharp[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#106)]  
  
3.  Passe o intervalo de um indicador para o `HideText` método, imprimir o documento e, em seguida, passar o mesmo intervalo para o `UnhideText` método.  
  
     O exemplo de código a seguir pode ser usado em uma personalização no nível de documento. Para usar este exemplo, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#107)]  
  
     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar o exemplo, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#107)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo de código pressupõe que o documento contém uma <xref:Microsoft.Office.Tools.Word.Bookmark> controle (em uma personalização no nível de documento) ou <xref:Microsoft.Office.Interop.Word.Bookmark> controle (em um suplemento VSTO) que é nomeado `bookmark1`.  
  
## <a name="see-also"></a>Consulte também  
 [Como: imprimir documentos programaticamente](../vsto/how-to-programmatically-print-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: programaticamente redefinir intervalos em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)   
 [Como: atualizar o texto do indicador de forma programática](../vsto/how-to-programmatically-update-bookmark-text.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  