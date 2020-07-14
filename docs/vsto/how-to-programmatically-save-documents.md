---
title: 'Como: salvar documentos programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving
- Word [Office development in Visual Studio], saving documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 464d131261ecfb0a64a3ca279007ff9332cdb2e4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537586"
---
# <a name="how-to-programmatically-save-documents"></a>Como: salvar documentos programaticamente

Há várias maneiras de salvar Microsoft Office documentos do Word. Você pode salvar um documento sem alterar o nome do documento ou pode salvar um documento com um novo nome.

[!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="save-a-document-without-changing-the-name"></a>Salvar um documento sem alterar o nome

### <a name="to-save-the-document-associated-with-a-document-level-customization"></a>Para salvar o documento associado a uma personalização no nível do documento

1. Chame o <xref:Microsoft.Office.Tools.Word.Document.Save%2A> método da <xref:Microsoft.Office.Tools.Word.Document> classe. Para usar este exemplo de código, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#7)]
     [!code-csharp[Trin_VstcoreWordAutomation#7](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#7)]

### <a name="to-save-the-active-document"></a>Para salvar o documento ativo

1. Chamar o <xref:Microsoft.Office.Interop.Word._Document.Save%2A> método para o documento ativo. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

    [!code-vb[Trin_VstcoreWordAutomation#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#8)]
    [!code-csharp[Trin_VstcoreWordAutomation#8](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#8)]

   Se você não tiver certeza se o documento que deseja salvar é o documento ativo, você pode consultá-lo por seu nome.

### <a name="to-save-a-document-specified-by-name"></a>Para salvar um documento especificado por nome

1. Use o nome do documento como um argumento para a <xref:Microsoft.Office.Interop.Word.Documents> coleção. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#9)]
     [!code-csharp[Trin_VstcoreWordAutomation#9](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#9)]

## <a name="save-a-document-with-a-new-name"></a>Salvar um documento com um novo nome

Use o `SaveAs` método para salvar um documento com um novo nome. Você pode usar esse método do <xref:Microsoft.Office.Tools.Word.Document> item de host em um projeto de palavra de nível de documento ou de um <xref:Microsoft.Office.Interop.Word.Document> objeto nativo em qualquer projeto do Word. Esse método requer que você especifique o novo nome de arquivo, mas outros argumentos são opcionais.

> [!NOTE]
> Se você mostrar a caixa de diálogo **salvar** como dentro do <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> manipulador de eventos de `ThisDocument` e definir o parâmetro *Cancel* como **false**, o aplicativo poderá ser fechado inesperadamente. Se você definir o parâmetro de *cancelamento* como **true**, será exibida uma mensagem de erro indicando que o salvamento automático foi desabilitado.

### <a name="to-save-the-document-associated-with-a-document-level-customization-with-a-new-name"></a>Para salvar o documento associado a uma personalização em nível de documento com um novo nome

1. Chame o `SaveAs` método da `ThisDocument` classe em seu projeto, usando um caminho totalmente qualificado e um nome de arquivo. Se um arquivo com esse nome já existir nessa pasta, ele será reescrito silenciosamente. Para usar este exemplo de código, execute-o da `ThisDocument` classe.

    > [!NOTE]
    > O `SaveAs` método lançará uma exceção se um diretório de destino não existir ou se houver outros problemas ao salvar um arquivo. É uma boa prática usar um `try...catch` bloco em volta do `SaveAs` método ou dentro de um método de chamada.

     [!code-vb[Trin_VstcoreWordAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#10)]
     [!code-csharp[Trin_VstcoreWordAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#10)]

### <a name="to-save-a-native-document-with-a-new-name"></a>Para salvar um documento nativo com um novo nome

1. Chame o <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> método do <xref:Microsoft.Office.Interop.Word.Document> que você deseja salvar, usando um caminho totalmente qualificado e um nome de arquivo. Se um arquivo com esse nome já existir nessa pasta, ele será reescrito silenciosamente.

     O exemplo de código a seguir salva o documento ativo com um novo nome. Para usar este exemplo de código, execute-o `ThisDocument` da `ThisAddIn` classe ou em seu projeto.

    > [!NOTE]
    > O <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> método lançará uma exceção se um diretório de destino não existir ou se houver outros problemas ao salvar um arquivo. É uma boa prática usar uma **tentativa... Catch** em volta do <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> método ou dentro de um método de chamada.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#10)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#10](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#10)]

## <a name="compile-the-code"></a>Compilar o código

Este exemplo de código requer o seguinte:

- Para salvar um documento por nome, um documento chamado *NewDocument.doc* deve existir em um diretório chamado *Test* na unidade C.

- Para salvar um documento com um novo nome, um diretório chamado *teste* deve existir na unidade C.

## <a name="see-also"></a>Consulte também

- [Como: fechar documentos programaticamente](../vsto/how-to-programmatically-close-documents.md)
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Item de host do documento](../vsto/document-host-item.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
