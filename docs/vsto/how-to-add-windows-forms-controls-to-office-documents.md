---
title: 'Como: adicionar controles dos Windows forms a documentos do Office'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], adding
- controls [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], Windows Forms controls
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7b5a6246a79d2d1f910b6ca39ce290f6c325dbe6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892747"
---
# <a name="how-to-add-windows-forms-controls-to-office-documents"></a>Como: adicionar controles dos Windows Forms a documentos do Office
  Você pode adicionar controles de formulários do Windows para o Microsoft Office Excel e documentos do Microsoft Office Word em tempo de design em projetos de nível de documento. Em tempo de execução, você pode adicionar controles em personalizações no nível de documento e nos suplementos do VSTO. Por exemplo, você pode adicionar um <xref:Microsoft.Office.Tools.Excel.Controls.ComboBox> controle à sua planilha para que os usuários podem selecionar em uma lista de opções.  
  
 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]  
  
 Este tópico descreve as seguintes tarefas:  
  
- [Adicionar controles em tempo de design](#designtime)  
  
- [Adicionar controles em tempo de execução em projetos de nível de documento](#runtimedoclevel)  
  
- [Adicionar controles em tempo de execução VSTO Add-ins](#runtimeaddin)  
  
  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como eu faço para: adicionar controles a um documento se surgir em tempo de execução?](http://go.microsoft.com/fwlink/?LinkId=132782).  
  
##  <a name="designtime"></a> Adicionar controles em tempo de design  
 Há várias maneiras de adicionar controles de formulários do Windows para o documento em um projeto de nível de documento em tempo de design.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
### <a name="to-drag-a-windows-forms-control-to-the-document"></a>Para arrastar um controle dos Windows Forms para o documento  
  
1.  Crie ou abra um projeto de pasta de trabalho do Excel ou documento do Word no Visual Studio, para que o documento está visível no designer. Para obter informações sobre a criação de projetos, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  No **controles comuns** guia da **caixa de ferramentas**, clique no controle que você deseja adicionar e arraste-o para o documento.  
  
    > [!NOTE]  
    >  Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
### <a name="to-draw-a-windows-forms-control-on-the-document"></a>Para desenhar um controle Windows Forms no documento  
  
1.  Crie ou abra um projeto de pasta de trabalho do Excel ou documento do Word no Visual Studio, para que o documento está visível no designer. Para obter informações sobre a criação de projetos, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  No **controles comuns** guia da **caixa de ferramentas**, clique no controle que você deseja adicionar.  
  
3.  No documento, clique onde você deseja que o canto superior esquerdo do controle a ser localizado e arraste até onde você deseja que o canto inferior direito do controle a ser localizado.  
  
     O controle é adicionado ao documento com a localização e tamanho especificados.  
  
    > [!NOTE]  
    >  Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
### <a name="to-add-a-windows-forms-control-to-the-document-by-single-clicking-the-control"></a>Para adicionar um controle de formulários do Windows ao documento, o controle clicando em único  
  
1.  Crie ou abra um projeto de pasta de trabalho do Excel ou documento do Word no Visual Studio, para que o documento está visível no designer. Para obter informações sobre a criação de projetos, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  No **controles comuns** guia da **caixa de ferramentas**, clique no controle que você deseja adicionar  
  
3.  Um documento, clique onde você deseja que o controle a ser adicionado.  
  
     O controle é adicionado ao documento com o tamanho padrão.  
  
    > [!NOTE]  
    >  Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
### <a name="to-add-a-windows-forms-control-to-the-document-by-double-clicking-the-control"></a>Para adicionar um controle de formulários do Windows para o documento clicando duas vezes no controle  
  
1.  Crie ou abra um projeto de pasta de trabalho do Excel ou documento do Word no Visual Studio, para que o documento está visível no designer. Para obter informações sobre a criação de projetos, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  No **controles comuns** guia da **caixa de ferramentas**, clique duas vezes no controle que você deseja adicionar.  
  
     O controle é adicionado ao documento no centro do documento ou painel ativo.  
  
    > [!NOTE]  
    >  Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
### <a name="to-add-a-windows-forms-control-to-the-document-by-pressing-the-enter-key"></a>Para adicionar um controle de formulários do Windows para o documento, pressionando a tecla Enter  
  
1.  Crie ou abra um projeto de pasta de trabalho do Excel ou documento do Word no Visual Studio, para que o documento está visível no designer. Para obter informações sobre a criação de projetos, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  No **controles comuns** guia da **caixa de ferramentas**, clique no controle que você deseja adicionar e, em seguida, pressione a **Enter** chave.  
  
     O controle é adicionado ao documento no centro do documento ou painel ativo.  
  
    > [!NOTE]  
    >  Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
##  <a name="runtimedoclevel"></a> Adicionar controles em tempo de execução em projetos de nível de documento  
 Você pode adicionar programaticamente os controles dos Windows Forms a um documento em tempo de execução. No Word, use os métodos das <xref:Microsoft.Office.Tools.Word.DocumentBase.Controls%2A> propriedade do `ThisDocument` classe. No Excel, use métodos do <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Controls%2A> propriedade de um `Sheet` *n* classe. Cada método tem várias sobrecargas que permitem que você especifique o local do controle de maneiras diferentes.  
  
 Quando você adiciona um controle dos Windows Forms a um documento em tempo de execução, o controle não é persistido no documento quando o documento é fechado. Você pode recriar o controle na próxima vez em que o documento é aberto. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
### <a name="to-add-a-windows-forms-control-at-runtime"></a>Para adicionar um controle dos Windows Forms em tempo de execução  
  
1.  Usar um método que tem o nome Add\<*classe de controle*> (em que *controlar classe* é o nome de classe do controle Windows Forms que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>).  
  
     O exemplo de código a seguir demonstra como adicionar um <xref:Microsoft.Office.Tools.Excel.Controls.Button> a célula **C5** de `Sheet1` em um projeto de nível de documento para Excel.  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#4](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#4)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#4)]  
  
##  <a name="runtimeaddin"></a> Adicionar controles em tempo de execução VSTO Add-ins  
 Você pode adicionar controles Windows Forms por meio de programação para qualquer documento aberto no tempo de execução. Primeiro, gere um item de host que se baseia em uma planilha ou um documento aberto. Em seguida, no Word, use os métodos do <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade do novo item de host. No Excel, use métodos do <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> propriedade do novo item de host. Cada método tem várias sobrecargas que permitem que você especifique o local do controle de maneiras diferentes.  
  
 Quando você adiciona um controle dos Windows Forms a um documento em tempo de execução, o controle não é persistido no documento quando o documento é fechado. Você pode recriar o controle na próxima vez em que o documento é aberto. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 Para obter mais informações sobre como gerar itens de host em projetos de suplemento do VSTO, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
### <a name="to-add-a-windows-forms-control-at-runtime"></a>Para adicionar um controle dos Windows Forms em tempo de execução  
  
1.  Usar um método que tem o nome Add\<*classe de controle*> (em que *controlar classe* é o nome de classe do controle Windows Forms que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>).  
  
    > [!NOTE]  
    >  No suplemento do VSTO projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve adicionar uma referência para o *Microsoft.Office.Tools.Excel.v4.0.Utilities.dll* ou *Microsoft.Office.Tools.Word.v4.0.Utilities.dll* assembly antes de poder acessar o Add\<*controlar classe*> métodos.  
  
     O exemplo de código a seguir demonstra como adicionar um <xref:Microsoft.Office.Tools.Word.Controls.Button> ao primeiro parágrafo do documento ativo, usando um suplemento do VSTO do Word.  
  
     [!code-vb[Trin_WordAddInDynamicControls#7](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#7)]
     [!code-csharp[Trin_WordAddInDynamicControls#7](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#7)]  
  
## <a name="see-also"></a>Consulte também  
 [Controles de formulários do Windows na visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Como: redimensionar controles dentro de células da planilha](../vsto/how-to-resize-controls-within-worksheet-cells.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  