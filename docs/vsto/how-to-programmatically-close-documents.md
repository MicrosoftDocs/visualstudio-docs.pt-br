---
title: 'Como: fechar documentos programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing
- Word [Office development in Visual Studio], closing documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9a846aded5d24f84fdaeac79a1bad6c61a3f5570
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257768"
---
# <a name="how-to-programmatically-close-documents"></a>Como: fechar documentos programaticamente
  Você pode fechar o documento ativo ou você pode especificar um documento ser fechado.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="close-the-active-document"></a>Fechar o documento ativo  
 Há dois procedimentos para fechar o documento ativo: uma para personalizações no nível de documento e uma para suplementos do VSTO.  
  
### <a name="to-close-the-active-document-in-a-document-level-customization"></a>Para fechar o documento ativo em uma personalização no nível de documento  
  
1.  Chame o <xref:Microsoft.Office.Tools.Word.Document.Close%2A> método da `ThisDocument` classe em seu projeto para fechar o documento associado com a personalização. Para usar o exemplo de código a seguir, executá-la na `ThisDocument` classe.  
  
    > [!NOTE]  
    >  Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> de valor para o *SaveChanges* parâmetro para fechar sem salvar as alterações ou solicitar que o usuário.  
  
     [!code-vb[Trin_VstcoreWordAutomation#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#3)]
     [!code-csharp[Trin_VstcoreWordAutomation#3](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#3)]  
  
### <a name="to-close-the-active-document-in-a-vsto-add-in"></a>Para fechar o documento ativo em um suplemento do VSTO  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word._Document.Close%2A> método da <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> propriedade para fechar o documento ativo. Para usar o exemplo de código a seguir, executá-la na `ThisAddIn` classe em seu projeto.  
  
    > [!NOTE]  
    >  Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> de valor para o *SaveChanges* parâmetro para fechar sem salvar as alterações ou solicitar que o usuário.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#3)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#3](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#3)]  
  
## <a name="close-a-document-that-you-specify-by-name"></a>Fechar um documento que você especifica por nome  
 A maneira que você fechar um documento que você especifica por nome é o mesmo para suplementos do VSTO e personalizações no nível do documento.  
  
### <a name="to-close-a-document-that-you-specify-by-name"></a>Para fechar um documento que você especifica por nome  
  
1.  Especifique o nome do documento como um argumento para o <xref:Microsoft.Office.Interop.Word._Application.Documents%2A> coleta e, em seguida, chame o <xref:Microsoft.Office.Interop.Word._Document.Close%2A> método. O exemplo de código a seguir pressupõe que um documento chamado **NewDocument** é aberto no Word.  
  
    > [!NOTE]  
    >  Este exemplo passa o <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> de valor para o *SaveChanges* parâmetro para fechar sem salvar as alterações ou solicitar que o usuário.  
  
     [!code-vb[Trin_VstcoreWordAutomation#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#4)]
     [!code-csharp[Trin_VstcoreWordAutomation#4](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#4)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)   
 [Como: salvar documentos programaticamente](../vsto/how-to-programmatically-save-documents.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  