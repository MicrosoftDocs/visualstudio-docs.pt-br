---
title: Como adicionar controles ListObject a planilhas
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ListObject control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c53d820170c359e568b0a7b0ab5711a632d9eba
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538314"
---
# <a name="how-to-add-listobject-controls-to-worksheets"></a>Como adicionar controles ListObject a planilhas
  Você pode adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles a uma Microsoft Office planilha do Excel em tempo de design e em tempo de execução em projetos de nível de documento.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Você também pode adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles em tempo de execução em projetos de suplemento do VSTO.

 Este tópico descreve as seguintes tarefas:

- [Adicionar controles ListObject em tempo de design](#designtime)

- [Adicionar controles ListObject em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Adicionar controles ListObject em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.ListObject> controles, consulte o [controle ListObject](../vsto/listobject-control.md).

## <a name="add-listobject-controls-at-design-time"></a><a name="designtime"></a>Adicionar controles ListObject em tempo de design
 Há várias maneiras de adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles a uma planilha em um projeto de nível de documento em tempo de design: de dentro do Excel, da **caixa de ferramentas**do Visual Studio e da janela fontes de **dados** .

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-use-the-ribbon-in-excel"></a>Para usar a faixa de faixas no Excel

1. Na guia **Inserir** , no grupo **tabelas** , clique em **tabela**.

2. Selecione a célula ou células que você deseja incluir na lista e clique em **OK**.

#### <a name="to-use-the-toolbox"></a>Para usar a caixa de ferramentas

1. Na guia **controles do Excel** da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Excel.ListObject> para a planilha.

     A caixa de diálogo **Adicionar controle ListObject** é exibida.

2. Selecione a célula ou células que você deseja incluir na lista e clique em **OK**.

     Se você não quiser manter o nome padrão, poderá alterar o nome na janela **Propriedades** .

#### <a name="to-use-the-data-sources-window"></a>Para usar a janela fontes de dados

1. Abra a janela **Data Sources** e crie uma fonte de dados para seu projeto. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

2. Arraste uma tabela da janela **fontes de dados** para sua planilha.

     Um controle associado a dados <xref:Microsoft.Office.Tools.Excel.ListObject> é adicionado à planilha. Para obter mais informações, consulte [vinculação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

## <a name="add-listobject-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>Adicionar controles ListObject em tempo de execução em um projeto de nível de documento
 Você pode adicionar o <xref:Microsoft.Office.Tools.Excel.ListObject> controle dinamicamente em tempo de execução. Isso permite que você crie os controles de host em resposta a eventos. Os objetos de lista criados dinamicamente não são mantidos na planilha como controles de host quando a planilha é fechada. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>Para adicionar um controle ListObject a uma planilha programaticamente

1. No <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos de `Sheet1` , insira o código a seguir para adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle às células **a1** a **a4**.

     [!code-csharp[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#2)]

## <a name="add-listobject-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>Adicionar controles ListObject em tempo de execução em um projeto de suplemento do VSTO
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle programaticamente a qualquer planilha aberta em um projeto de suplemento do VSTO. Os objetos de lista criados dinamicamente não são mantidos na planilha como controles de host quando a planilha é salva e fechada. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>Para adicionar um controle ListObject a uma planilha programaticamente

1. O código a seguir gera um item de host de planilha baseado na planilha aberta e, em seguida, adiciona um <xref:Microsoft.Office.Tools.Excel.ListObject> controle às células **a1** a **a4**.

     [!code-csharp[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#8)]
     [!code-vb[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#8)]

## <a name="see-also"></a>Confira também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Como: redimensionar controles de ListObject](../vsto/how-to-resize-listobject-controls.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
