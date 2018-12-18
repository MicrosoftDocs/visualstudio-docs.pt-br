---
title: 'Como: abrir documentos existentes programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: dd9e120283c392978a21fa9f796f9eed5e3dab31
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258717"
---
# <a name="how-to-programmatically-open-existing-documents"></a>Como: abrir documentos existentes programaticamente
  O <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> método abre o documento do Microsoft Office Word existente, especificado por um nome de arquivo e caminho totalmente qualificado. Esse método retorna um <xref:Microsoft.Office.Interop.Word.Document> que representa o documento aberto.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-open-a-document"></a>Para abrir um documento  
  
-   Chame o <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> método da <xref:Microsoft.Office.Interop.Word.Documents> coleta e fornecer um caminho para o documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#5)]  
  
## <a name="to-open-a-document-as-read-only"></a>Para abrir um documento como somente leitura  
  
-   Chamar o <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> método, fornecer um caminho para o documento e definir o *ReadOnly* argumento **True** na chamada do método.  
  
     [!code-vb[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#6)]
     [!code-csharp[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#6)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo de código requer o seguinte:  
  
-   Um documento chamado *NewDocument.doc* deve existir em um diretório chamado *teste* na unidade C.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar novos documentos programaticamente](../vsto/how-to-programmatically-create-new-documents.md)   
 [Como: fechar documentos programaticamente](../vsto/how-to-programmatically-close-documents.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  