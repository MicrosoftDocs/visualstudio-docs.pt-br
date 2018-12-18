---
title: 'Como: adicionar conteúdo controles a documentos do Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- DropDownListContentControl, adding to documents
- BuildingBlockGalleryContentControl, adding to documents
- partial document protection [Office development in Visual Studio]
- RichTextContentControl, adding to documents
- Word [Office development in Visual Studio], partial document protection
- content controls [Office development in Visual Studio], protecting
- PictureContentControl, adding to documents
- GroupContentControl, adding to documents
- document protection [Office development in Visual Studio]
- PlainTextContentControl, adding to documents
- content controls [Office development in Visual Studio], adding
- ComboBoxContentControl, adding to documents
- DatePickerContentControl, adding to documents
- Word [Office development in Visual Studio], restricted permissions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f654efacace3e4b7cbdfff8919309a09d4a544ff
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936960"
---
# <a name="how-to-add-content-controls-to-word-documents"></a>Como: adicionar conteúdo controles a documentos do Word
  Em projetos em nível de documento do Word, você pode adicionar controles de conteúdo para o documento em seu projeto em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO do Word, você pode adicionar controles de conteúdo para qualquer documento aberto no tempo de execução.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Este tópico descreve as seguintes tarefas:  
  
- [Adicionar controles de conteúdo em tempo de design](#designtime)  
  
- [Adicionar controles de conteúdo em tempo de execução em um projeto de nível de documento](#runtimedoclevel)  
  
- [Adicionar controles de conteúdo em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)  
  
  Para obter informações sobre controles de conteúdo, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
##  <a name="designtime"></a> Adicionar conteúdo a controles em tempo de design  
 Há várias maneiras de adicionar controles de conteúdo para o documento em um projeto de nível de documento em tempo de design:  
  
- Adicionar um controle de conteúdo do **controles do Word** guia o **caixa de ferramentas**.  
  
- Adicionar um controle de conteúdo ao documento da mesma maneira, você adicionaria o controle de conteúdo nativo no Word.  
  
- Arraste um controle de conteúdo para seu documento a partir de **fontes de dados** janela. Isso é útil quando você deseja associar o controle a dados quando o controle é criado. Para obter mais informações, consulte [como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md) e [como: preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-content-control-to-a-document-by-using-the-toolbox"></a>Para adicionar um controle de conteúdo a um documento usando a caixa de ferramentas  
  
1.  No documento que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, coloque o cursor onde você deseja adicionar o controle de conteúdo, ou selecione o texto que você deseja substituir o controle de conteúdo.  
  
2.  Abra o **caixa de ferramentas** e clique no **controles do Word** guia.  
  
3.  Adicione o controle em uma das seguintes maneiras:  
  
    -   Clique duas vezes em um controle de conteúdo a **caixa de ferramentas**.  
  
         ou  
  
    -   Clique em um controle de conteúdo a **caixa de ferramentas** e, em seguida, pressione a **Enter** chave.  
  
         ou  
  
    -   Arraste um controle de conteúdo do **caixa de ferramentas** ao documento. O controle de conteúdo é adicionado na seleção atual no documento, não no local do ponteiro do mouse.  
  
> [!NOTE]  
>  Não é possível adicionar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> usando o **caixa de ferramentas**. Você só pode adicionar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> no Word ou em tempo de execução.  
  
> [!NOTE]  
>  Visual Studio não fornece um controle de conteúdo da caixa de seleção na caixa de ferramentas. Para adicionar um controle de caixa de seleção de conteúdo ao documento, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> por meio de programação do objeto. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
#### <a name="to-add-a-content-control-to-a-document-in-word"></a>Para adicionar um controle de conteúdo a um documento do Word  
  
1.  No documento que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, coloque o cursor onde você deseja adicionar o controle de conteúdo, ou selecione o texto que você deseja substituir o controle de conteúdo.  
  
2.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
3.  No **controles** de grupo, clique no ícone para o controle de conteúdo que você deseja adicionar.  
  
##  <a name="runtimedoclevel"></a> Adicionar controles de conteúdo em tempo de execução em um projeto de nível de documento  
 Você pode adicionar controles de conteúdo por meio de programação ao documento em tempo de execução usando métodos das <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade do `ThisDocument` classe em seu projeto. Cada método tem três sobrecargas que você pode usar para adicionar um controle de conteúdo das seguintes maneiras:  
  
- Adicione um controle na seleção atual.  
  
- Adicione um controle em um intervalo especificado.  
  
- Adicione um controle com base em um controle de conteúdo nativo no documento.  
  
  Criados dinamicamente o conteúdo de controles não são mantidos no documento quando o documento é fechado. No entanto, um controle de conteúdo nativo permanece no documento. Você pode recriar um controle de conteúdo com base em um controle de conteúdo nativo na próxima vez em que o documento é aberto. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
> [!NOTE]  
>  Para adicionar um controle de conteúdo da caixa de seleção a um documento em um projeto do Word 2010, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
### <a name="to-add-a-content-control-at-the-current-selection"></a>Para adicionar um controle de conteúdo na seleção atual  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome de classe do controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um único parâmetro para o nome do novo controle.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `AddRichTextControlAtSelection` método o `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#700](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#700)]
     [!code-vb[Trin_ContentControlReference#700](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#700)]  
  
### <a name="to-add-a-content-control-at-a-specified-range"></a>Para adicionar um controle de conteúdo em um intervalo especificado  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tenha um <xref:Microsoft.Office.Interop.Word.Range> parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `AddRichTextControlAtRange` método o `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#701](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#701)]
     [!code-vb[Trin_ContentControlReference#701](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#701)]  
  
### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>Para adicionar um controle de conteúdo com base em um controle de conteúdo nativo  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tenha um `Microsoft.Office.Interop.Word.ContentControl` parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para criar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para cada controle nativo em rich text no documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `CreateRichTextControlsFromNativeControls` método o `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#702](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#702)]
     [!code-vb[Trin_ContentControlReference#702](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#702)]  
  
##  <a name="runtimeaddin"></a> Adicionar controles de conteúdo em tempo de execução em um projeto de suplemento do VSTO  
 Você pode adicionar controles de conteúdo por meio de programação para qualquer documento aberto no tempo de execução usando um suplemento do VSTO. Para fazer isso, gerar uma <xref:Microsoft.Office.Tools.Word.Document> hospedar o item que se baseia em um documento aberto e, em seguida, usar métodos do <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade deste item de host. Cada método tem três sobrecargas que você pode usar para adicionar um controle de conteúdo das seguintes maneiras:  
  
- Adicione um controle na seleção atual.  
  
- Adicione um controle em um intervalo especificado.  
  
- Adicione um controle com base em um controle de conteúdo nativo no documento.  
  
  Criados dinamicamente o conteúdo de controles não são mantidos no documento quando o documento é fechado. No entanto, um controle de conteúdo nativo permanece no documento. Você pode recriar um controle de conteúdo com base em um controle de conteúdo nativo na próxima vez em que o documento é aberto. Para obter mais informações, consulte [persistir controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).  
  
  Para obter mais informações sobre como gerar itens de host em projetos de suplemento do VSTO, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
> [!NOTE]  
>  Para adicionar um controle de conteúdo da caixa de seleção a um documento, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
### <a name="to-add-a-content-control-at-the-current-selection"></a>Para adicionar um controle de conteúdo na seleção atual  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome de classe do controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um único parâmetro para o nome do novo controle.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento ativo. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `AddRichTextControlAtSelection` método o `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#1)]  
  
### <a name="to-add-a-content-control-at-a-specified-range"></a>Para adicionar um controle de conteúdo em um intervalo especificado  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tenha um <xref:Microsoft.Office.Interop.Word.Range> parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento ativo. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `AddRichTextControlAtRange` método o `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#2)]  
  
#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>Para adicionar um controle de conteúdo com base em um controle de conteúdo nativo  
  
1.  Use uma <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *controlar classe*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tenha um `Microsoft.Office.Interop.Word.ContentControl` parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para criar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para todos os controles nativos em rich text que está em um documento, após o documento é aberto. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#3)]  
  
     Para c#, você também deve anexar a `Application_DocumentOpen` manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> eventos.  
  
     [!code-csharp[Trin_WordAddInDynamicControls#6](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#6)]  
  
## <a name="see-also"></a>Consulte também  
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)  
  