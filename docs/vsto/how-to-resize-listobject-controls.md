---
title: 'Como: redimensionar controles de ListObject'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- ListObject control, resizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 68a9841d8471189538959a311bf9349199d55f78
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545828"
---
# <a name="how-to-resize-listobject-controls"></a>Como: redimensionar controles de ListObject
  Você define o tamanho de um <xref:Microsoft.Office.Tools.Excel.ListObject> controle ao adicioná-lo a uma Microsoft Office pasta de trabalho do Excel; no entanto, talvez você queira redimensioná-lo posteriormente. Por exemplo, talvez você queira alterar uma lista de duas colunas para três colunas.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Você pode redimensionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles em tempo de design ou em tempo de execução em projetos de nível de documento. Você pode redimensionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles em tempo de execução em um projeto de suplemento do VSTO.

 Este tópico descreve as seguintes tarefas:

- [Redimensionar controles ListObject em tempo de design](#designtime)

- [Redimensionar controles ListObject em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Redimensionar controles ListObject em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.ListObject> controles, consulte o [controle ListObject](../vsto/listobject-control.md).

## <a name="resize-a-listobject-control-at-design-time"></a><a name="designtime"></a>Redimensionar um controle ListObject no tempo de design
 Para redimensionar uma lista, você pode clicar e arrastar uma das alças de dimensionamento ou pode redefinir seu tamanho na caixa de diálogo **redimensionar lista** .

### <a name="to-resize-a-list-by-using-the-resize-list-dialog-box"></a>Para redimensionar uma lista usando a caixa de diálogo redimensionar lista

1. Clique em qualquer lugar na <xref:Microsoft.Office.Tools.Excel.ListObject> tabela. A guia Design das **ferramentas de tabela**  >  **Design** na faixa de faixas é exibida.

2. Na seção Propriedades, clique em **redimensionar tabela**.

    ![VSTO_ResizeTable](../vsto/media/vsto-resizetable.png)

3. Selecione o novo intervalo de dados para a tabela.

4. Clique em **OK**.

## <a name="resize-a-listobject-control-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>Redimensionar um controle ListObject em tempo de execução em um projeto de nível de documento
 Você pode redimensionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle em tempo de execução usando o <xref:Microsoft.Office.Tools.Excel.ListObject.Resize%2A> método. Você não pode usar esse método para mover o <xref:Microsoft.Office.Tools.Excel.ListObject> controle para um novo local na planilha. Os cabeçalhos devem permanecer na mesma linha e o controle redimensionado <xref:Microsoft.Office.Tools.Excel.ListObject> deve sobrepor o objeto de lista original. O controle redimensionado <xref:Microsoft.Office.Tools.Excel.ListObject> deve conter uma linha de cabeçalho e pelo menos uma linha de dados.

### <a name="to-resize-a-list-object-programmatically"></a>Para redimensionar um objeto de lista programaticamente

1. Crie um <xref:Microsoft.Office.Tools.Excel.ListObject> controle que abranja a célula **a1** a **B3** em `Sheet1` .

     [!code-csharp[Trin_VstcoreHostControlsExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#6)]
     [!code-vb[Trin_VstcoreHostControlsExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#6)]

2. Redimensione a lista para incluir as células **a1** a **C5**.

     [!code-csharp[Trin_VstcoreHostControlsExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#7)]
     [!code-vb[Trin_VstcoreHostControlsExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#7)]

## <a name="resize-a-listobject-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>Redimensionar um ListObject em tempo de execução em um projeto de suplemento do VSTO
 Você pode redimensionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle em qualquer planilha aberta em tempo de execução. Para obter mais informações sobre como adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle a uma planilha usando um suplemento do VSTO, consulte [como: adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md).

### <a name="to-resize-a-list-object-programmatically"></a>Para redimensionar um objeto de lista programaticamente

1. Crie um <xref:Microsoft.Office.Tools.Excel.ListObject> controle que abranja a célula **a1** a **B3** em `Sheet1` .

     [!code-csharp[Trin_Excel_Dynamic_Controls#12](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#12)]
     [!code-vb[Trin_Excel_Dynamic_Controls#12](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#12)]

2. Redimensione a lista para incluir as células **a1** a **C5**.

     [!code-csharp[Trin_Excel_Dynamic_Controls#13](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#13)]
     [!code-vb[Trin_Excel_Dynamic_Controls#13](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#13)]

## <a name="see-also"></a>Confira também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Como adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [Como: redimensionar controles de indicador](../vsto/how-to-resize-bookmark-controls.md)
- [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)
