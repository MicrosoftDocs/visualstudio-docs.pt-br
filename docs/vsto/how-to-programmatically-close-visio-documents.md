---
title: 'Como: fechar documentos do Visio por meio de programação'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing Visio documents
- Visio [Office development in Visual Studio], closing Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 478905a8ba4dacd2102c4b19fe091016a7409773
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547479"
---
# <a name="how-to-programmatically-close-visio-documents"></a>Como: fechar documentos do Visio por meio de programação
  Você pode fechar o documento do Active Microsoft Office Visio usando o `Microsoft.Office.Interop.Visio.Document.Close` método.

 Para obter detalhes sobre esse método, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document. Método Close](/office/vba/api/Visio.Document.Close) .

## <a name="close-the-active-document"></a>Fechar o documento ativo

### <a name="to-close-the-active-document"></a>Para fechar o documento ativo

- Chame o `Microsoft.Office.Interop.Visio.Document.Close` método para fechar o documento ativo.

     Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Visio.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
- [Como: imprimir documentos do Visio programaticamente](../vsto/how-to-programmatically-print-visio-documents.md)
