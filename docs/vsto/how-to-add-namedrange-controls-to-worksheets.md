---
title: 'Como: adicionar controles NamedRange a planilhas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, adding to worksheets
- NamedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 448a44c8f4bc9380a4ef1ebfec33b264e797cac8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543514"
---
# <a name="how-to-add-namedrange-controls-to-worksheets"></a>Como: adicionar controles NamedRange a planilhas
  Você pode adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles a uma Microsoft Office planilha do Excel em tempo de design e em tempo de execução em projetos de nível de documento.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Você também pode adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles em tempo de execução em projetos de suplemento do VSTO.

 Este tópico descreve as seguintes tarefas:

- [Adicionar controles NamedRange em tempo de design](#designtime)

- [Adicionar controles NamedRange em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Adicionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.NamedRange> controles, consulte [controle NamedRange](../vsto/namedrange-control.md).

## <a name="add-namedrange-controls-at-design-time"></a><a name="designtime"></a>Adicionar controles NamedRange em tempo de design
 Há várias maneiras de adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles a uma planilha em um projeto de nível de documento em tempo de design: de dentro do Excel, da **caixa de ferramentas**do Visual Studio e da janela fontes de **dados** .

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-name-box-in-excel"></a>Para adicionar um controle NamedRange a uma planilha usando a caixa nome no Excel

1. Selecione a célula ou células que você deseja incluir no intervalo nomeado.

2. Na **caixa nome**, digite um nome para o intervalo e pressione **Enter**.

     A **caixa nome** está localizada ao lado da barra de fórmulas, logo acima **da coluna a** da planilha.

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-toolbox"></a>Para adicionar um controle NamedRange a uma planilha usando a caixa de ferramentas

1. Abra a **caixa de ferramentas** e clique na guia **controles do Excel** .

2. Clique <xref:Microsoft.Office.Tools.Excel.NamedRange> e arraste-o para uma planilha.

     A caixa de diálogo **Adicionar intervalo nomeado** é exibida.

3. Selecione a célula ou células que você deseja incluir no intervalo nomeado.

4. Clique em **OK**.

     Se você não quiser o nome padrão fornecido ao controle, poderá alterar o nome na janela **Propriedades** .

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-data-sources-window"></a>Para adicionar um controle NamedRange a uma planilha usando a janela fontes de dados

1. Abra a janela **Data Sources** e crie uma fonte de dados para seu projeto. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

2. Arraste um único campo da janela **fontes de dados** para sua planilha.

     Um controle associado a dados <xref:Microsoft.Office.Tools.Excel.NamedRange> é adicionado à planilha. Para obter mais informações, consulte [vinculação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

## <a name="add-namedrange-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>Adicionar controles NamedRange em tempo de execução em um projeto de nível de documento
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle programaticamente à sua planilha em tempo de execução. Isso permite que você crie os controles de host em resposta a eventos. Os intervalos nomeados criados dinamicamente não são mantidos na planilha como controles de host quando a planilha é fechada. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>Para adicionar um controle NamedRange a uma planilha programaticamente

1. No <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos de `Sheet1` , insira o código a seguir para adicionar o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle à célula **a1** e defina sua <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade como`Hello world!`

     [!code-csharp[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#3)]

## <a name="add-namedrange-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>Adicionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle programaticamente a qualquer planilha aberta em um projeto de suplemento do VSTO. Os intervalos nomeados criados dinamicamente não são mantidos na planilha como controles de host quando a planilha é fechada. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>Para adicionar um controle NamedRange a uma planilha programaticamente

1. O código a seguir gera um item de host de planilha baseado na planilha aberta e, em seguida, adiciona um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle à célula **a1** e define sua <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade como `Hello world` .

     [!code-csharp[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#7)]
     [!code-vb[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#7)]

## <a name="see-also"></a>Confira também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
