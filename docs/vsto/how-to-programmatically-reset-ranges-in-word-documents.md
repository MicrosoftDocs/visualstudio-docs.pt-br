---
title: 'Como: programaticamente redefinir intervalos em documentos do Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], resetting ranges
- ranges, resetting in documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0da42b0e6ad6f8761e474292532728beb3987c57
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669950"
---
# <a name="how-to-programmatically-reset-ranges-in-word-documents"></a>Como: programaticamente redefinir intervalos em documentos do Word
  Use o <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> método para redimensionar um intervalo existente em um documento do Microsoft Office Word.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-reset-an-existing-range"></a>Para redefinir um intervalo existente  
  
1.  Defina um intervalo inicial, começando com os sete primeiros caracteres no documento.  
  
     O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#43)]  
  
     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#43)]  
  
2.  Use <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> para iniciar o intervalo em que a segunda frase e encerrá-lo no final da sentença quinto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#44)]
     [!code-csharp[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#44)]  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização no nível de documento  
  
### <a name="to-reset-an-existing-range-in-a-document-level-customization"></a>Para redefinir um intervalo existente em uma personalização no nível de documento  
  
1.  O exemplo a seguir mostra o exemplo completo para uma personalização no nível de documento. Para usar esse código, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#42)]  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="to-reset-an-existing-range-in-a-vsto-add-in"></a>Para redefinir um intervalo existente em um suplemento do VSTO  
  
1.  O exemplo a seguir mostra o exemplo completo para um suplemento do VSTO. Para usar esse código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#42)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: estender programaticamente os intervalos em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: recuperar caracteres iniciais e finais em intervalos de forma programática](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)   
 [Como: programaticamente recolher intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)  
  
  