---
title: 'Como: atualizar o texto do indicador programaticamente'
description: Saiba como você pode usar o Visual Studio para inserir texto programaticamente em um marcador de espaço reservado em um documento do Microsoft Word.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, updating text
- text [Office development in Visual Studio], updating in bookmarks
- Bookmark control, updating contents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f67dbbe4d1d5c24d617f9cbc49a58ec2d134e90b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826194"
---
# <a name="how-to-programmatically-update-bookmark-text"></a>Como: atualizar o texto do indicador programaticamente
  Você pode inserir texto em um marcador de espaço reservado em um Microsoft Office documento do Word para que você possa recuperar o texto mais tarde ou substituir o texto em um indicador. Se você estiver desenvolvendo uma personalização em nível de documento, também poderá atualizar o texto em um <xref:Microsoft.Office.Tools.Word.Bookmark> controle associado aos dados. Para obter mais informações, consulte [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 O objeto de indicador pode ser um dos dois tipos:

- Um <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host.

   <xref:Microsoft.Office.Tools.Word.Bookmark> os controles estendem <xref:Microsoft.Office.Interop.Word.Bookmark> objetos nativos habilitando a vinculação de dados e expondo eventos. Para obter mais informações sobre controles de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

- Um objeto <xref:Microsoft.Office.Interop.Word.Bookmark> nativo.

   <xref:Microsoft.Office.Interop.Word.Bookmark> os objetos não têm recursos ou funcionalidades de associação de dados.

  Quando você atribui texto a um indicador, o comportamento difere entre a <xref:Microsoft.Office.Interop.Word.Bookmark> e a <xref:Microsoft.Office.Tools.Word.Bookmark> . Para obter mais informações, consulte [controle de indicadores](../vsto/bookmark-control.md).

## <a name="use-host-controls"></a>Usar controles de host

### <a name="to-update-bookmark-contents-using-a-bookmark-control"></a>Para atualizar o conteúdo do indicador usando um controle de indicador

1. Crie um procedimento que usa um `bookmark` argumento para o nome do indicador e um `newText` argumento para a cadeia de caracteres a ser atribuída à <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> propriedade.

    > [!NOTE]
    > A atribuição de texto à <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> propriedade ou <xref:Microsoft.Office.Tools.Word.Bookmark.FormattedText%2A> de um <xref:Microsoft.Office.Tools.Word.Bookmark> controle não faz com que o indicador seja excluído.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet63":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet63":::

2. Atribua a cadeia de caracteres *TextoNovo* à <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> Propriedade do <xref:Microsoft.Office.Tools.Word.Bookmark> .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet64":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet64":::

## <a name="use-word-objects"></a>Usar objetos do Word

### <a name="to-update-bookmark-contents-using-a-word-bookmark-object"></a>Para atualizar o conteúdo do indicador usando um objeto de indicador do Word

1. Crie um procedimento que tenha um `bookmark` argumento para o nome do <xref:Microsoft.Office.Interop.Word.Bookmark> e um `newText` argumento para a cadeia de caracteres a ser atribuída à <xref:Microsoft.Office.Interop.Word.Range.Text%2A> Propriedade do indicador.

    > [!NOTE]
    > A atribuição de texto a um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto do Word nativo faz com que o indicador seja excluído.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet65":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet65":::

2. Atribua a cadeia de caracteres *TextoNovo* à <xref:Microsoft.Office.Interop.Word.Range.Text%2A> Propriedade do indicador, que exclui automaticamente o indicador. Em seguida, adicione novamente o indicador à <xref:Microsoft.Office.Interop.Word.Bookmarks> coleção.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet66":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet66":::

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet66":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet66":::

## <a name="see-also"></a>Consulte também
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Controle de indicador](../vsto/bookmark-control.md)
