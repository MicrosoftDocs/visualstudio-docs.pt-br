---
title: 'Como: fechar documentos do Visio por meio de programação'
description: Saiba como você pode fechar o documento do Active Microsoft Office Visio usando o Microsoft.Office.Interop.Visio.Document. Método Close.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8802cc34555fcb695c5554209255cb8fd9f154c2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825297"
---
# <a name="how-to-programmatically-close-visio-documents"></a>Como: fechar documentos do Visio por meio de programação
  Você pode fechar o documento do Active Microsoft Office Visio usando o `Microsoft.Office.Interop.Visio.Document.Close` método.

 Para obter detalhes sobre esse método, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document. Método Close](/office/vba/api/Visio.Document.Close) .

## <a name="close-the-active-document"></a>Fechar o documento ativo

### <a name="to-close-the-active-document"></a>Para fechar o documento ativo

- Chame o `Microsoft.Office.Interop.Visio.Document.Close` método para fechar o documento ativo.

     Para usar o exemplo de código a seguir, execute-o na `ThisAddIn` classe em um projeto de suplemento do VSTO para Visio.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
- [Como: imprimir documentos do Visio programaticamente](../vsto/how-to-programmatically-print-visio-documents.md)
