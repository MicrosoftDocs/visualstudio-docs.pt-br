---
title: 'Como: redimensionar controles NamedRange'
description: Saiba como você pode usar o Visual Studio para redimensionar programaticamente os controles NamedRange em uma pasta de trabalho do Microsoft Excel.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- NamedRange control, resizing
- ranges, resizing in Excel
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3b70b34de222c35903a4f08b95d9efe8d8f896d9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826454"
---
# <a name="how-to-resize-namedrange-controls"></a>Como: redimensionar controles NamedRange
  Você pode definir o tamanho de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ao adicioná-lo a um Microsoft Office documento do Excel; no entanto, talvez você queira redimensioná-lo posteriormente.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Você pode redimensionar um intervalo nomeado em tempo de design ou em tempo de execução em projetos de nível de documento. Você também pode redimensionar intervalos nomeados em tempo de execução em suplementos do VSTO no nível de aplicativo.

 Este tópico descreve as seguintes tarefas:

- [Redimensionar controles NamedRange em tempo de design](#designtime)

- [Redimensionar controles NamedRange em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Redimensionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

## <a name="resize-namedrange-controls-at-design-time"></a><a name="designtime"></a> Redimensionar controles NamedRange em tempo de design
 Você pode redimensionar um intervalo nomeado redefinindo seu tamanho na caixa de diálogo **definir nome** .

### <a name="to-resize-a-named-range-by-using-the-define-name-dialog-box"></a>Para redimensionar um intervalo nomeado usando a caixa de diálogo Definir nome

1. Clique com o botão direito do mouse em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.

2. Clique em **gerenciar intervalos nomeados** no menu de atalho.

     A caixa de diálogo **definir nome** é exibida.

3. Selecione o intervalo nomeado que você deseja redimensionar.

4. Desmarque a caixa **refere-se a** .

5. Selecione as células que você deseja usar para definir o tamanho do intervalo nomeado.

6. Clique em **OK**.

## <a name="resize-namedrange-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> Redimensionar controles NamedRange em tempo de execução em um projeto de nível de documento
 Você pode redimensionar um intervalo nomeado programaticamente usando a <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> propriedade.

> [!NOTE]
> Na janela **Propriedades** , a <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> propriedade é marcada como somente leitura.

### <a name="to-resize-a-named-range-programmatically"></a>Para redimensionar um intervalo nomeado programaticamente

1. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na célula **a1** de `Sheet1` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet4":::

2. Redimensione o intervalo nomeado para incluir a célula **B1**.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet5":::

## <a name="resize-namedrange-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a> Redimensionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO
 Você pode redimensionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle em qualquer planilha aberta em tempo de execução. Para obter mais informações sobre como adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a uma planilha usando um suplemento do VSTO, consulte [como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md).

### <a name="to-resize-a-named-range-programmatically"></a>Para redimensionar um intervalo nomeado programaticamente

1. Crie um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na célula **a1** de `Sheet1` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet10":::

2. Redimensione o intervalo nomeado para incluir a célula **B1**.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet11":::

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Como: redimensionar controles de indicador](../vsto/how-to-resize-bookmark-controls.md)
- [Como: redimensionar controles de ListObject](../vsto/how-to-resize-listobject-controls.md)
