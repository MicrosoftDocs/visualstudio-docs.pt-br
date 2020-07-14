---
title: Proteger documentos e partes de documentos de forma programática
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document protection
- documents [Office development in Visual Studio], document protection
- Word documents, protection
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4654a2c218470e0d5e2a1ddd54a88de5c4546f7b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537833"
---
# <a name="how-to-programmatically-protect-documents-and-parts-of-documents"></a>Como: proteger documentos e partes de documentos programaticamente
  Você pode adicionar proteção a Microsoft Office documentos do Word para impedir que os usuários façam qualquer edição no documento.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Você também pode marcar determinadas áreas do documento como exceções, de modo que os usuários especificados possam editar apenas as áreas do documento. Por exemplo, talvez você queira proteger um documento inteiro, exceto um indicador específico. Opcionalmente, você pode adicionar uma senha para que os usuários não possam remover a proteção do documento, a menos que saibam a senha.

> [!NOTE]
> O exemplo a seguir não usa proteção por senha; no entanto, talvez você queira considerar o uso de uma senha ao adicionar a proteção do documento. Para obter mais informações, consulte a amostra do protetor de documento em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

 Você também pode usar controles de conteúdo para proteger partes de documentos. Para obter mais informações, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).

## <a name="protect-a-document-that-is-part-of-a-document-level-customization"></a>Proteger um documento que faz parte de uma personalização no nível do documento

### <a name="to-protect-a-document-that-is-part-of-a-document-level-customization"></a>Para proteger um documento que faz parte de uma personalização em nível de documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> método da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]

### <a name="to-exclude-a-bookmark-control-from-document-protection"></a>Para excluir um controle de indicador da proteção de documentos

1. Proteja todo o documento usando o <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> método.

     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]

2. Exclua `Bookmark1` da proteção de documento.

     [!code-vb[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#112)]
     [!code-csharp[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#112)]

### <a name="compile-the-code"></a>Compilar o código
 Para usar esses exemplos de código, execute-os a partir da `ThisDocument` classe em seu projeto. Esses exemplos de código pressupõem que você tenha um <xref:Microsoft.Office.Tools.Word.Bookmark> controle existente chamado `Bookmark1` no documento no qual esse código é exibido.

## <a name="protect-a-document-by-using-a-vsto-add-in"></a>Proteger um documento usando um suplemento do VSTO

### <a name="to-protect-a-document-by-using-an-application-level-vsto-add-in"></a>Para proteger um documento usando um suplemento do VSTO em nível de aplicativo

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.Protect%2A> método do <xref:Microsoft.Office.Interop.Word.Document> que você deseja proteger.

     O exemplo de código a seguir protege o documento ativo. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#111)]

## <a name="see-also"></a>Confira também
- [Proteção de documentos em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)
- [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)
- [Como: permitir que o código execute por trás de documentos com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
