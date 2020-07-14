---
title: 'Como: redefinição de intervalos programaticamente em documentos do Word'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], resetting ranges
- ranges, resetting in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f1978a280a26af3b2a21e0bc5a4c9a238a723a9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547115"
---
# <a name="how-to-programmatically-reset-ranges-in-word-documents"></a>Como: redefinição de intervalos programaticamente em documentos do Word
  Use o <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> método para redimensionar um intervalo existente em um Microsoft Office documento do Word.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-reset-an-existing-range"></a>Para redefinir um intervalo existente

1. Defina um intervalo inicial começando com os primeiros sete caracteres no documento.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     [!code-vb[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#43)]

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#43)]

2. Use <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> para iniciar o intervalo na segunda frase e termine-o no final da quinta frase.

     [!code-vb[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#44)]
     [!code-csharp[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#44)]

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-reset-an-existing-range-in-a-document-level-customization"></a>Para redefinir um intervalo existente em uma personalização no nível do documento

1. O exemplo a seguir mostra o exemplo completo para uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#42)]

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-reset-an-existing-range-in-a-vsto-add-in"></a>Para redefinir um intervalo existente em um suplemento do VSTO

1. O exemplo a seguir mostra o exemplo completo para um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#42)]

## <a name="see-also"></a>Confira também
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como recuperar programaticamente caracteres de início e término em intervalos](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [Como: reduzir programaticamente intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
