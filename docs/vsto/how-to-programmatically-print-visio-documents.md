---
title: 'Como: imprimir documentos do Visio programaticamente'
description: Saiba como você pode imprimir um documento completo do Microsoft Visio ou apenas imprimir uma página específica nesse documento.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 13e18b1d1e20c836be740a6b44a591be6df6e926
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827182"
---
# <a name="how-to-programmatically-print-visio-documents"></a>Como: imprimir documentos do Visio programaticamente
  Você pode imprimir um documento completo Microsoft Office Visio ou apenas uma página específica.

 Para obter detalhes sobre os métodos de impressão, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document. Método Print](/office/vba/api/Visio.Document.Print) e [Microsoft. Office. Interop. Visio. Page. Print](/office/vba/api/Visio.Page.Print) .

## <a name="print-a-visio-document"></a>Imprimir um documento do Visio

### <a name="to-print-a-complete-document"></a>Para imprimir um documento completo

- Chame o `Microsoft.Office.Interop.Visio.Document.Print` método do `Microsoft.Office.Interop.Visio.Document` objeto que você deseja imprimir.

     O exemplo de código a seguir imprime o documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet8":::

## <a name="print-a-page-of-a-visio-document"></a>Imprimir uma página de um documento do Visio

### <a name="to-print-a-page-of-a-document"></a>Para imprimir uma página de um documento

- Chame o `Microsoft.Office.Interop.Visio.Pages.Print` método do `Microsoft.Office.Interop.Visio.Pages` objeto que você deseja imprimir.

     O exemplo de código a seguir imprime a primeira página do documento ativo. Para usar este exemplo, execute o código da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet9":::

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: fechar documentos do Visio por meio de programação](../vsto/how-to-programmatically-close-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
