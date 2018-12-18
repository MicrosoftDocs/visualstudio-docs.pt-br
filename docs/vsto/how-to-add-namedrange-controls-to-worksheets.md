---
title: 'Como: adicionar controles NamedRange a planilhas'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, adding to worksheets
- NamedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 35febfa4c4d13b3f5d3d279f7d1c35e96051d54b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867111"
---
# <a name="how-to-add-namedrange-controls-to-worksheets"></a>Como: adicionar controles NamedRange a planilhas
  Você pode adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles a uma planilha do Microsoft Office Excel em tempo de design e em tempo de execução em projetos de nível de documento.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Você também pode adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles em tempo de execução em projetos de suplemento do VSTO.  
  
 Este tópico descreve as seguintes tarefas:  
  
- [Adicionar controles NamedRange em tempo de design](#designtime)  
  
- [Adicionar controles NamedRange em tempo de execução em um projeto de nível de documento](#runtimedoclevel)  
  
- [Adicionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)  
  
  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.NamedRange> controles, consulte [controle NamedRange](../vsto/namedrange-control.md).  
  
##  <a name="designtime"></a> Adicionar controles NamedRange em tempo de design  
 Há várias maneiras de adicionar <xref:Microsoft.Office.Tools.Excel.NamedRange> controles em uma planilha em um projeto de nível de documento em tempo de design: de dentro do Excel, do Visual Studio **caixa de ferramentas**e para o **fontes de dados** janela.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-name-box-in-excel"></a>Para adicionar um controle NamedRange para uma planilha usando a caixa de nome no Excel  
  
1.  Selecione a célula ou células que você deseja incluir no intervalo nomeado.  
  
2.  No **caixa de nome**, digite um nome para o intervalo e pressione **Enter**.  
  
     O **caixa de nome** está localizado ao lado da barra de fórmulas, logo acima de coluna **um** da planilha.  
  
### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-toolbox"></a>Para adicionar um controle NamedRange para uma planilha usando a caixa de ferramentas  
  
1.  Abra o **caixa de ferramentas** e clique no **Excel controles** guia.  
  
2.  Clique em <xref:Microsoft.Office.Tools.Excel.NamedRange> e arraste-o para uma planilha.  
  
     O **adicionar intervalo de nomeado** caixa de diálogo é exibida.  
  
3.  Selecione a célula ou células que você deseja incluir no intervalo nomeado.  
  
4.  Clique em **OK**.  
  
     Se você não quiser que o nome padrão que é fornecido para o controle, você pode alterar o nome na **propriedades** janela.  
  
### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-data-sources-window"></a>Para adicionar um controle NamedRange para uma planilha usando a janela fontes de dados  
  
1.  Abra o **fontes de dados** janela e criar uma fonte de dados para seu projeto. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).  
  
2.  Arraste um campo único do **fontes de dados** janela à sua planilha.  
  
     Uma associação de dados <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é adicionado à planilha. Para obter mais informações, consulte [vinculação de dados e o Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).  
  
##  <a name="runtimedoclevel"></a> Adicionar controles NamedRange em tempo de execução em um projeto de nível de documento  
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle por meio de programação à sua planilha em tempo de execução. Isso permite que você crie os controles de host em resposta a eventos. Criado dinamicamente intervalos nomeados não são mantidos na planilha que os controles de host quando a planilha é fechada. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>Para adicionar um controle NamedRange a uma planilha programaticamente  
  
1.  No <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos do `Sheet1`, insira o código a seguir para adicionar o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a célula **A1** e defina seu <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade para `Hello world!`  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#3)]  
  
##  <a name="runtimeaddin"></a> Adicionar controles NamedRange em tempo de execução em um projeto de suplemento do VSTO  
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle programaticamente para qualquer planilha aberta em um projeto de suplemento do VSTO. Criado dinamicamente intervalos nomeados não são mantidos na planilha que os controles de host quando a planilha é fechada. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>Para adicionar um controle NamedRange a uma planilha programaticamente  
  
1.  O código a seguir gera um item de host de planilha que se baseia na planilha de aberto e, em seguida, adiciona uma <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a célula **A1** e define seu <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade `Hello world`.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#7)]
     [!code-vb[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#7)]  
  
## <a name="see-also"></a>Consulte também  
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  