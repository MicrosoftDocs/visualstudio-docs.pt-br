---
title: 'Como: adicionar controles ListObject a planilhas'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ListObject control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 402e7f80ea208d714b31bd61e25b352494310487
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949246"
---
# <a name="how-to-add-listobject-controls-to-worksheets"></a>Como: adicionar controles ListObject a planilhas
  Você pode adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles a uma planilha do Microsoft Office Excel em tempo de design e em tempo de execução em projetos de nível de documento.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Você também pode adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles em tempo de execução em projetos de suplemento do VSTO.  
  
 Este tópico descreve as seguintes tarefas:  
  
- [Adicionar controles ListObject em tempo de design](#designtime)  
  
- [Adicionar controles ListObject em tempo de execução em um projeto de nível de documento](#runtimedoclevel)  
  
- [Adicionar controles ListObject em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)  
  
  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Excel.ListObject> controles, consulte [controle ListObject](../vsto/listobject-control.md).  
  
##  <a name="designtime"></a> Adicionar controles ListObject em tempo de design  
 Há várias maneiras de adicionar <xref:Microsoft.Office.Tools.Excel.ListObject> controles em uma planilha em um projeto de nível de documento em tempo de design: de dentro do Excel, do Visual Studio **caixa de ferramentas**e para o **fontes de dados** janela.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
### <a name="to-use-the-ribbon-in-excel"></a>Usar a faixa de opções no Excel  
  
1.  Sobre o **inserir** guia da **tabelas** , clique em **tabela**.  
  
2.  Selecione a célula ou células que você deseja incluir na lista e clique em **Okey**.  
  
#### <a name="to-use-the-toolbox"></a>Para usar a caixa de ferramentas  
  
1.  Dos **controles do Excel** guia da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Excel.ListObject> à planilha.  
  
     O **adicionar controle do ListObject** caixa de diálogo é exibida.  
  
2.  Selecione a célula ou células que você deseja incluir na lista e clique em **Okey**.  
  
     Se você não deseja manter o nome padrão, você pode alterar o nome na **propriedades** janela.  
  
#### <a name="to-use-the-data-sources-window"></a>Usar a janela fontes de dados  
  
1.  Abra o **fontes de dados** janela e criar uma fonte de dados para seu projeto. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).  
  
2.  Arraste uma tabela das **fontes de dados** janela à sua planilha.  
  
     Uma associação de dados <xref:Microsoft.Office.Tools.Excel.ListObject> controle é adicionado à planilha. Para obter mais informações, consulte [vinculação de dados e o Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).  
  
##  <a name="runtimedoclevel"></a> Adicionar controles ListObject em tempo de execução em um projeto de nível de documento  
 Você pode adicionar o <xref:Microsoft.Office.Tools.Excel.ListObject> controle dinamicamente em tempo de execução. Isso permite que você crie os controles de host em resposta a eventos. Lista criada dinamicamente objetos não são mantidos na planilha que os controles de host quando a planilha é fechada. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>Para adicionar um controle ListObject a uma planilha programaticamente  
  
1.  No <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> manipulador de eventos do `Sheet1`, insira o código a seguir para adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle às células **A1** por meio de **A4**.  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#2)]  
  
##  <a name="runtimeaddin"></a> Adicionar controles ListObject em tempo de execução em um projeto de suplemento do VSTO  
 Você pode adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle programaticamente para qualquer planilha aberta em um projeto de suplemento do VSTO. Lista criada dinamicamente objetos não são mantidos na planilha que os controles de host quando a planilha for salvo e, em seguida, fechada. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>Para adicionar um controle ListObject a uma planilha programaticamente  
  
1.  O código a seguir gera um item de host de planilha que se baseia na planilha de aberto e, em seguida, adiciona uma <xref:Microsoft.Office.Tools.Excel.ListObject> controle às células **A1** por meio **A4**.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#8)]
     [!code-vb[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#8)]  
  
## <a name="see-also"></a>Consulte também  
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Controle ListObject](../vsto/listobject-control.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Como: redimensionar controles ListObject](../vsto/how-to-resize-listobject-controls.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  