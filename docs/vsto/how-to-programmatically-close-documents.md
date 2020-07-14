---
title: 'Como: fechar documentos programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing
- Word [Office development in Visual Studio], closing documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 18dc4099f4c1df17efbe2dd3c213332bb73b52c4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547453"
---
# <a name="how-to-programmatically-close-documents"></a>Como: fechar documentos programaticamente
  Você pode fechar o documento ativo ou pode especificar um documento a ser fechado.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="close-the-active-document"></a>Fechar o documento ativo
 Há dois procedimentos para fechar o documento ativo: um para personalizações em nível de documento e outro para os suplementos do VSTO.

### <a name="to-close-the-active-document-in-a-document-level-customization"></a>Para fechar o documento ativo em uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.Close%2A> método da `ThisDocument` classe em seu projeto para fechar o documento associado à personalização. Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe.

    > [!NOTE]
    > Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> valor para o parâmetro *SaveChanges* para fechar sem salvar as alterações ou solicitar o usuário.

     [!code-vb[Trin_VstcoreWordAutomation#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#3)]
     [!code-csharp[Trin_VstcoreWordAutomation#3](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#3)]

### <a name="to-close-the-active-document-in-a-vsto-add-in"></a>Para fechar o documento ativo em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.Close%2A> método da <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> propriedade para fechar o documento ativo. Para usar o exemplo de código a seguir, execute-o da `ThisAddIn` classe em seu projeto.

    > [!NOTE]
    > Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> valor para o parâmetro *SaveChanges* para fechar sem salvar as alterações ou solicitar o usuário.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#3)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#3](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#3)]

## <a name="close-a-document-that-you-specify-by-name"></a>Fechar um documento que você especificar por nome
 A maneira de fechar um documento que você especifica por nome é a mesma para suplementos do VSTO e personalizações em nível de documento.

### <a name="to-close-a-document-that-you-specify-by-name"></a>Para fechar um documento que você especifica por nome

1. Especifique o nome do documento como um argumento para a <xref:Microsoft.Office.Interop.Word._Application.Documents%2A> coleção e, em seguida, chame o <xref:Microsoft.Office.Interop.Word._Document.Close%2A> método. O exemplo de código a seguir pressupõe que um documento chamado **NewDocument** está aberto no Word.

    > [!NOTE]
    > Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> valor para o parâmetro *SaveChanges* para fechar sem salvar as alterações ou solicitar o usuário.

     [!code-vb[Trin_VstcoreWordAutomation#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#4)]
     [!code-csharp[Trin_VstcoreWordAutomation#4](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#4)]

## <a name="see-also"></a>Confira também
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Como: salvar documentos programaticamente](../vsto/how-to-programmatically-save-documents.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
