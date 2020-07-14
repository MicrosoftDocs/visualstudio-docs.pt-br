---
title: 'Como: imprimir documentos do Visio programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], printing Visio documents
- documents [Office development in Visual Studio], printing Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0e31a55e49d42311b5ec5fff82769584cc55ce09
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537794"
---
# <a name="how-to-programmatically-print-visio-documents"></a>Como: imprimir documentos do Visio programaticamente
  Você pode imprimir um documento completo Microsoft Office Visio ou apenas uma página específica.

 Para obter detalhes sobre os métodos de impressão, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document. Método Print](/office/vba/api/Visio.Document.Print) e [Microsoft. Office. Interop. Visio. Page. Print](/office/vba/api/Visio.Page.Print) .

## <a name="print-a-visio-document"></a>Imprimir um documento do Visio

### <a name="to-print-a-complete-document"></a>Para imprimir um documento completo

- Chame o `Microsoft.Office.Interop.Visio.Document.Print` método do `Microsoft.Office.Interop.Visio.Document` objeto que você deseja imprimir.

     O exemplo de código a seguir imprime o documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#8)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#8)]

## <a name="print-a-page-of-a-visio-document"></a>Imprimir uma página de um documento do Visio

### <a name="to-print-a-page-of-a-document"></a>Para imprimir uma página de um documento

- Chame o `Microsoft.Office.Interop.Visio.Pages.Print` método do `Microsoft.Office.Interop.Visio.Pages` objeto que você deseja imprimir.

     O exemplo de código a seguir imprime a primeira página do documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#9)]

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: fechar documentos do Visio por meio de programação](../vsto/how-to-programmatically-close-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
