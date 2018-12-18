---
title: 'Como: proteger documentos e partes de documentos de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document protection
- documents [Office development in Visual Studio], document protection
- Word documents, protection
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9acef141944b106a9bace38fef8ede7041bfecc5
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669773"
---
# <a name="how-to-programmatically-protect-documents-and-parts-of-documents"></a>Como: proteger documentos e partes de documentos de forma programática
  Você pode adicionar proteção para documentos do Microsoft Office Word para impedir que usuários fazendo nenhuma edição ao documento.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Você também pode marcar determinadas áreas do documento como exceções para que os usuários especificados podem editar somente essas áreas do documento. Por exemplo, você talvez queira proteger um documento inteiro, exceto para um indicador específico. Opcionalmente, você pode adicionar uma senha para que os usuários não é possível remover a proteção do documento, a menos que eles conhecem a senha.  
  
> [!NOTE]  
>  O exemplo a seguir não usa a proteção por senha; No entanto, você talvez queira considerar o uso de uma senha ao adicionar a proteção do documento. Para obter mais informações, consulte o exemplo de documento protetor em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
 Você também pode usar controles de conteúdo para proteger partes de documentos. Para obter mais informações, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).  
  
## <a name="protect-a-document-that-is-part-of-a-document-level-customization"></a>Proteger um documento que faz parte de uma personalização no nível de documento  
  
### <a name="to-protect-a-document-that-is-part-of-a-document-level-customization"></a>Para proteger um documento que faz parte de uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> método da `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]  
  
### <a name="to-exclude-a-bookmark-control-from-document-protection"></a>Para excluir um controle de indicador da proteção de documento  
  
1.  Proteger o documento inteiro usando o <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> método.  
  
     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]  
  
2.  Excluir `Bookmark1` da proteção de documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#112)]
     [!code-csharp[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#112)]  
  
### <a name="compile-the-code"></a>Compilar o código  
 Para usar esses exemplos de código, executá-los pelo `ThisDocument` classe em seu projeto. Estes exemplos de código supõem que você tiver uma <xref:Microsoft.Office.Tools.Word.Bookmark> controle chamado `Bookmark1` no documento em que esse código é exibida.  
  
## <a name="protect-a-document-by-using-a-vsto-add-in"></a>Proteger um documento por meio de um suplemento do VSTO  
  
### <a name="to-protect-a-document-by-using-an-application-level-vsto-add-in"></a>Para proteger um documento por meio de um suplemento do VSTO do nível de aplicativo  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word._Document.Protect%2A> método da <xref:Microsoft.Office.Interop.Word.Document> que você deseja proteger.  
  
     O exemplo de código a seguir protege o documento ativo. Para usar este exemplo de código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#111)]  
  
## <a name="see-also"></a>Consulte também  
 [Proteção do documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Como: permitir que o código execute documentos code-behind com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)   
 [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  