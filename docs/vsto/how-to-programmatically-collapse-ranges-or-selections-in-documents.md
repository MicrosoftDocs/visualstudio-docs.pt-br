---
title: Recolher intervalos ou seleções em documentos programaticamente
description: Saiba que, se você estiver trabalhando com um intervalo ou um objeto de seleção, talvez queira alterar a seleção para um ponto de inserção antes de inserir texto.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- selections, collapsing
- documents [Office development in Visual Studio], collapsing ranges
- collapsing selections
- ranges, collapsing
- collapsing ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5d1fb41943690da5144fb06245ed7f4aa70250aa
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828638"
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>Como: reduzir programaticamente intervalos ou seleções em documentos
  Se você estiver trabalhando com um <xref:Microsoft.Office.Interop.Word.Range> <xref:Microsoft.Office.Interop.Word.Selection> objeto ou, talvez queira alterar a seleção para um ponto de inserção antes de inserir texto, para evitar substituir o texto existente. Os <xref:Microsoft.Office.Interop.Word.Range> objetos e <xref:Microsoft.Office.Interop.Word.Selection> têm um método Collapse, que utiliza os <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> valores de enumeração:

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> recolhe a seleção até o início da seleção. Esse será o padrão se você não especificar um valor de enumeração.

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> recolhe a seleção até o final da seleção.

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-collapse-a-range-and-insert-new-text"></a>Para recolher um intervalo e inserir um novo texto

1. Crie um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste no primeiro parágrafo do documento.

    O exemplo de código a seguir pode ser usado em uma personalização em nível de documento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet46":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet46":::

    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet46":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet46":::

2. Use o <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> valor de enumeração para recolher o intervalo.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet47":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet47":::

3. Insira o novo texto.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet48":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet48":::

4. Selecione o <xref:Microsoft.Office.Interop.Word.Range>.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet49":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet49":::

   Se você usar o <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> valor de enumeração, o texto será inserido no início do parágrafo a seguir.

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet50":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet50":::

   Você pode esperar que a inserção de uma nova frase a insira antes do marcador de parágrafo, mas que não é o caso porque o intervalo original inclui o marcador de parágrafo. Para obter mais informações, consulte [como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md).

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="to-collapse-a-range-in-a-document-level-customization"></a>Para recolher um intervalo em uma personalização no nível do documento

1. O exemplo a seguir mostra o método completo para uma personalização em nível de documento. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet45":::

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="to-collapse-a-range-in-a-vsto-add-in"></a>Para recolher um intervalo em um suplemento do VSTO

1. O exemplo a seguir mostra o método completo para um suplemento do VSTO. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet45":::

## <a name="see-also"></a>Consulte também
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Como: definir e selecionar intervalos de forma programática em documentos](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Como recuperar programaticamente caracteres de início e término em intervalos](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [Como: estender intervalos programaticamente em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [Como: redefinição de intervalos programaticamente em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
