---
title: 'Como: abrir documentos do Visio programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening Visio documents
- Visio [Office development in Visual Studio], opening Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb21d201c282461cbe82005f56bed023bb022209
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519984"
---
# <a name="how-to-programmatically-open-visio-documents"></a>Como: abrir documentos do Visio programaticamente
  Há dois métodos para abrir documentos existentes do Microsoft Office Visio: Open e OpenEx. O método OpenEx é idêntico ao método Open, exceto pelo fato de que ele fornece argumentos nos quais o chamador pode especificar como o documento é aberto.

 Para obter detalhes sobre o modelo de objeto, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Documents. Método Open](/office/vba/api/Visio.Documents.Open) e [Microsoft.Office.Interop.Visio.Documents. Método OpenEx](/office/vba/api/Visio.Documents.OpenEx) .

## <a name="open-a-visio-document"></a>Abrir um documento do Visio

### <a name="to-open-a-visio-document"></a>Para abrir um documento do Visio

- Chame o `Microsoft.Office.Interop.Visio.Documents.Open` método e forneça o caminho totalmente qualificado do documento do Visio.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#5](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#5)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#5](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#5)]

## <a name="open-a-visio-document-with-specified-arguments"></a>Abrir um documento do Visio com argumentos especificados

### <a name="to-open-a-visio-document-as-read-only-and-docked"></a>Para abrir um documento do Visio como somente leitura e encaixado

- Chame o `Microsoft.Office.Interop.Visio.Documents.OpenEx` método, forneça o caminho totalmente qualificado do documento do Visio e inclua os argumentos que você deseja usar — nesse caso, encaixado e somente leitura.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#6)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código requer o seguinte:

- Um documento do Visio chamado `myDrawing.vsd` deve estar localizado em um diretório chamado `Test` na pasta *meus documentos* (para o Windows XP e versões anteriores) ou a pasta *documentos* (para o Windows Vista).

## <a name="see-also"></a>Confira também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: fechar documentos do Visio por meio de programação](../vsto/how-to-programmatically-close-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
- [Como: imprimir documentos do Visio programaticamente](../vsto/how-to-programmatically-print-visio-documents.md)
