---
title: 'Como: adicionar controles de gráfico a planilhas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fdb1f738fe6e68f7470ae65e6ce08b2f3be0ef6d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546231"
---
# <a name="how-to-add-chart-controls-to-worksheets"></a>Como: adicionar controles de gráfico a planilhas
  Você pode adicionar <xref:Microsoft.Office.Tools.Excel.Chart> controles a uma Microsoft Office planilha do Excel em tempo de design e em tempo de execução em personalizações em nível de documento. Você também pode adicionar <xref:Microsoft.Office.Tools.Excel.Chart> controles em tempo de execução em suplementos do VSTO.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Este tópico descreve as seguintes tarefas:

- [Adicionar controles de gráfico em tempo de design](#designtime)

- [Adicionar controles de gráfico em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Adicionar controles de gráfico em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.Chart> controles, consulte [controle de gráfico](../vsto/chart-control.md).

## <a name="add-chart-controls-at-design-time"></a><a name="designtime"></a>Adicionar controles de gráfico em tempo de design
 Você pode adicionar o <xref:Microsoft.Office.Tools.Excel.Chart> controle à sua planilha da mesma maneira que adicionaria um gráfico de dentro do aplicativo.

> [!NOTE]
> O <xref:Microsoft.Office.Tools.Excel.Chart> controle não está disponível na **caixa de ferramentas** ou na janela fontes de **dados** .

### <a name="to-add-a-chart-host-control-to-a-worksheet-in-excel"></a>Para adicionar um controle de host de gráfico a uma planilha no Excel

1. Na guia **Inserir** , no grupo **gráficos** , clique em **coluna**, clique em uma categoria de gráficos e, em seguida, clique no tipo de gráfico desejado.

2. Na caixa de diálogo **Inserir gráfico** , clique em **OK**.

3. Na guia **design** , no grupo de **dados** , clique em **selecionar dados**.

4. Na caixa de diálogo **selecionar fonte de dados** , clique na caixa **intervalo de dados** do **gráfico** e desmarque qualquer seleção padrão.

5. Na folha **dados para o gráfico** , selecione o intervalo de células que contém os dados do gráfico (células **a5** a **D8**).

6. Na caixa de diálogo **selecionar fonte de dados** , clique em **OK**.

## <a name="add-chart-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>Adicionar controles de gráfico em tempo de execução em um projeto de nível de documento
 Você pode adicionar o <xref:Microsoft.Office.Tools.Excel.Chart> controle dinamicamente em tempo de execução. Os gráficos criados dinamicamente não são persistidos no documento como controles de host quando o documento é fechado. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>Para adicionar um controle de gráfico a uma planilha programaticamente

1. No <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos de `Sheet1` , insira o código a seguir para adicionar o <xref:Microsoft.Office.Tools.Excel.Chart> controle.

     [!code-csharp[Trin_VstcoreHostControlsExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#1)]
     [!code-vb[Trin_VstcoreHostControlsExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#1)]

## <a name="add-chart-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>Adicionar controles de gráfico em tempo de execução em um projeto de suplemento do VSTO
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.Chart> controle programaticamente a qualquer planilha aberta em um projeto de suplemento do VSTO. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

 Os controles de gráfico criados dinamicamente não são persistidos na planilha como controles de host quando a planilha é fechada. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>Para adicionar um controle de gráfico a uma planilha programaticamente

1. O código a seguir gera um item de host de planilha baseado na planilha aberta e, em seguida, adiciona um <xref:Microsoft.Office.Tools.Excel.Chart> controle.

     [!code-csharp[Trin_Excel_Dynamic_Controls#9](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#9)]
     [!code-vb[Trin_Excel_Dynamic_Controls#9](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#9)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo tem os seguintes requisitos:

- Dados a serem colocados em gráfico, armazenados no intervalo de a5 a D8 na planilha.

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Controle de gráfico](../vsto/chart-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
