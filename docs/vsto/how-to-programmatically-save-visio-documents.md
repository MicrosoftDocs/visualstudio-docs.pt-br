---
title: 'Como: salvar documentos do Visio programaticamente'
description: Saiba como você pode usar o Visual Studio para salvar programaticamente documentos existentes do Microsoft Visio e novos documentos que ainda não foram salvos.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving Visio documents
- Visio [Office development in Visual Studio], saving Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 340d813a19c0c0dc5c347d3cfe4c7b29ff1bd049
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828989"
---
# <a name="how-to-programmatically-save-visio-documents"></a>Como: salvar documentos do Visio programaticamente
  Há várias maneiras de salvar Microsoft Office documentos do Visio:

- Salvar alterações em um documento existente.

- Salve um novo documento ou salve um documento com um novo nome.

- Salvar um documento com argumentos especificados.

  Para obter mais informações, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document. Método Save](/office/vba/api/Visio.Document.Save) , [Microsoft.Office.Interop.Visio.Document. Método SaveAs](/office/vba/api/Visio.Document.SaveAs) e [Microsoft.Office.Interop.Visio.Document. Método SaveAsEx](/office/vba/api/Visio.Document.SaveAsEx) .

## <a name="save-an-existing-document"></a>Salvar um documento existente

### <a name="to-save-a-document"></a>Para salvar um documento

- Chame o `Microsoft.Office.Interop.Visio.Document.Save` método da `Microsoft.Office.Tools.Visio.Document` classe de um documento que foi salvo anteriormente.

     Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

    > [!NOTE]
    > O `Microsoft.Office.Interop.Visio.Document.Save` método lançará uma exceção se um novo documento do Visio ainda não tiver sido salvo.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet11":::

## <a name="save-a-document-with-a-new-name"></a>Salvar um documento com um novo nome
 Use o `Microsoft.Office.Interop.Visio.Document.SaveAs` método para salvar um novo documento ou um documento que tenha um novo nome. Esse método requer que você especifique o novo nome de arquivo.

### <a name="to-save-the-active-visio-document-with-a-new-name"></a>Para salvar o documento ativo do Visio com um novo nome

- Chame o `Microsoft.Office.Interop.Visio.Document.SaveAs` método do `Microsoft.Office.Tools.Visio.Document` que você deseja salvar, usando um caminho totalmente qualificado, incluindo um nome de arquivo. Se um arquivo com esse nome já existir nessa pasta, ele será reescrito silenciosamente.

     Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet10":::

## <a name="save-a-document-with-a-new-name-and-specified-arguments"></a>Salvar um documento com um novo nome e argumentos especificados
 Use o `Microsoft.Office.Interop.Visio.Document.SaveAsEx` método para salvar um documento com um novo nome e especifique os argumentos aplicáveis a serem aplicados ao documento.

### <a name="to-save-document-with-a-new-name-and-specified-arguments"></a>Para salvar o documento com um novo nome e argumentos especificados

- Chame o `Microsoft.Office.Interop.Visio.Document.SaveAsEx` método do `Microsoft.Office.Tools.Visio.Document` que você deseja salvar, usando um caminho totalmente qualificado, incluindo um nome de arquivo. Se um arquivo com esse nome já existir nessa pasta, uma exceção será lançada.

     O exemplo de código a seguir salva o documento ativo com um novo nome, marca o documento como somente leitura e mostra o documento na lista de documentos usada mais recentemente. Para usar este exemplo de código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet12":::

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código requer o seguinte:

- Para salvar um documento que tem um novo nome, um diretório chamado `Test` deve estar localizado na pasta *meus documentos* (para o Windows XP e versões anteriores) ou a pasta *documentos* (para o Windows Vista).

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como criar programaticamente novos documentos do Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: fechar documentos do Visio por meio de programação](../vsto/how-to-programmatically-close-visio-documents.md)
- [Como: imprimir documentos do Visio programaticamente](../vsto/how-to-programmatically-print-visio-documents.md)
