---
title: 'Como: adicionar controles de indicador a documentos do Word'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.Bookmark.Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Bookmark control, adding to documents
- Create Bookmark Control dialog box
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: de5868674790239b8374ef9796308280588ae96e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547245"
---
# <a name="how-to-add-bookmark-controls-to-word-documents"></a>Como: adicionar controles de indicador a documentos do Word
  Em projetos de nível de documento, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles ao documento em seu projeto em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles a qualquer documento aberto em tempo de execução.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Este tópico descreve as seguintes tarefas:

- [Adicionar controles de indicador em tempo de design](#designtime)

- [Adicionar controles de indicador em tempo de execução em um projeto de nível de documento](#runtimedoclevel)

- [Adicionar controles de indicador em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)

  Para obter mais informações sobre <xref:Microsoft.Office.Tools.Word.Bookmark> controles, consulte [controle de indicadores](../vsto/bookmark-control.md).

## <a name="add-bookmark-controls-at-design-time"></a><a name="designtime"></a>Adicionar controles de indicador em tempo de design
 Há várias maneiras de adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles ao documento em um projeto de nível de documento em tempo de design:

- Na **caixa de ferramentas**do Visual Studio.

   Você pode arrastar o <xref:Microsoft.Office.Tools.Word.Bookmark> controle da **caixa de ferramentas** para seu documento. Talvez você queira escolher dessa forma se já estiver usando a caixa de **ferramentas** para adicionar Windows Forms controles ao seu documento.

- De dentro do Word.

   Você pode adicionar o <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao documento da mesma maneira que adicionaria o indicador nativo. A vantagem de adicioná-lo dessa forma é que você pode nomear seu controle no momento em que criá-lo.

- Na janela **fontes de dados** .

   Você pode arrastar o <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o documento na janela **fontes de dados** . Isso é útil quando você deseja associar o controle aos dados ao mesmo tempo. Você pode adicionar o controle de host da mesma maneira que adicionaria um controle de formulário do Windows da janela **fontes de dados** . Para obter mais informações, consulte [vinculação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

#### <a name="to-add-a-bookmark-control-to-a-document-from-the-toolbox"></a>Para adicionar um controle de indicador a um documento da caixa de ferramentas

1. Abra a **caixa de ferramentas** e clique na guia **controles do Word** .

2. Arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o documento.

     A caixa de diálogo **Adicionar indicador** é exibida.

3. Selecione o texto ou outros itens que você deseja incluir no indicador.

4. Clique em **OK**.

     Se você não quiser manter o nome do indicador padrão, poderá alterar o nome na janela **Propriedades** .

#### <a name="to-add-a-bookmark-control-to-a-document-in-word"></a>Para adicionar um controle de indicador a um documento no Word

1. No documento que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer, coloque o cursor onde você deseja adicionar o indicador ou selecione o texto que você deseja que o indicador Coloque.

2. Na guia **Inserir** da faixa de faixas, no grupo **links** , clique no botão **indicador** .

3. Na caixa de diálogo **indicador** , digite o nome do novo indicador e clique em **Adicionar**.

## <a name="add-bookmark-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>Adicionar controles de indicador em tempo de execução em um projeto de nível de documento
 Você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles programaticamente ao seu documento em tempo de execução usando métodos da <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade da `ThisDocument` classe em seu projeto. Há duas sobrecargas de método que você pode usar para adicionar um <xref:Microsoft.Office.Tools.Word.Bookmark> controle das seguintes maneiras:

- Adicione um <xref:Microsoft.Office.Tools.Word.Bookmark> em um intervalo especificado.

- Adicione um <xref:Microsoft.Office.Tools.Word.Bookmark> que se baseia em um indicador nativo no documento (ou seja, a <xref:Microsoft.Office.Interop.Word.Bookmark> ).

  Controles criados dinamicamente <xref:Microsoft.Office.Tools.Word.Bookmark> não são persistidos no documento quando o documento é fechado. No entanto, um nativo <xref:Microsoft.Office.Interop.Word.Bookmark> permanece no documento. Você pode recriar um <xref:Microsoft.Office.Tools.Word.Bookmark> que se baseia em um indicador nativo na próxima vez em que o documento for aberto. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

#### <a name="to-add-a-bookmark-control-to-a-document-programmatically"></a>Para adicionar um controle de indicador a um documento programaticamente

1. No `ThisDocument_Startup` manipulador de eventos em seu projeto, insira o código a seguir para adicionar o <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao primeiro parágrafo do documento.

     [!code-csharp[Trin_VstcoreHostControlsWord#1](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#1)]
     [!code-vb[Trin_VstcoreHostControlsWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#1)]

    > [!NOTE]
    > Se você quiser criar um <xref:Microsoft.Office.Tools.Word.Bookmark> controle de um existente <xref:Microsoft.Office.Interop.Word.Bookmark> , use o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddBookmark%2A> método e passe o existente <xref:Microsoft.Office.Interop.Word.Bookmark> .

## <a name="add-bookmark-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>Adicionar controles de indicador em tempo de execução em um projeto de suplemento do VSTO
 Você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles programaticamente a qualquer documento aberto em tempo de execução usando um suplemento do VSTO. Para fazer isso, gere um <xref:Microsoft.Office.Tools.Word.Document> item de host baseado em um documento aberto e, em seguida, use os métodos da <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade desse item de host. Há duas sobrecargas de método que você pode usar para adicionar um <xref:Microsoft.Office.Tools.Word.Bookmark> controle das seguintes maneiras:

- Adicione um <xref:Microsoft.Office.Tools.Word.Bookmark> em um intervalo especificado.

- Adicione um <xref:Microsoft.Office.Tools.Word.Bookmark> que se baseia em um indicador nativo no documento (ou seja, a <xref:Microsoft.Office.Interop.Word.Bookmark> ).

  Controles criados dinamicamente <xref:Microsoft.Office.Tools.Word.Bookmark> não são persistidos no documento quando o documento é fechado. No entanto, um nativo <xref:Microsoft.Office.Interop.Word.Bookmark> permanece no documento. Você pode recriar um <xref:Microsoft.Office.Tools.Word.Bookmark> que se baseia em um indicador nativo na próxima vez em que o documento for aberto. Para obter mais informações, consulte [manter controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).

  Para obter mais informações sobre como gerar itens de host em projetos de suplemento do VSTO, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

#### <a name="to-add-a-bookmark-control-at-a-specified-range"></a>Para adicionar um controle de indicador em um intervalo especificado

1. Use o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddBookmark%2A> método e passe o <xref:Microsoft.Office.Interop.Word.Range> onde você deseja adicionar o <xref:Microsoft.Office.Tools.Word.Bookmark> .

     O exemplo de código a seguir adiciona um novo no <xref:Microsoft.Office.Tools.Word.Bookmark> início do documento ativo. Para usar este exemplo, execute o código do `ThisAddIn_Startup` manipulador de eventos em um projeto de suplemento do VSTO do Word.

     [!code-vb[Trin_WordAddInDynamicControls#4](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#4)]
     [!code-csharp[Trin_WordAddInDynamicControls#4](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#4)]

#### <a name="to-add-a-bookmark-control-that-is-based-on-a-native-bookmark-control"></a>Para adicionar um controle de indicador baseado em um controle de indicador nativo

1. Use o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddBookmark%2A> método e passe o existente <xref:Microsoft.Office.Interop.Word.Bookmark> que você deseja usar como base para o novo <xref:Microsoft.Office.Tools.Word.Bookmark> .

     O exemplo de código a seguir cria um novo <xref:Microsoft.Office.Tools.Word.Bookmark> com base no primeiro <xref:Microsoft.Office.Interop.Word.Bookmark> no documento ativo. Para usar este exemplo, execute o código do `ThisAddIn_Startup` manipulador de eventos em um projeto de suplemento do VSTO do Word.

     [!code-vb[Trin_WordAddInDynamicControls#5](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#5)]
     [!code-csharp[Trin_WordAddInDynamicControls#5](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#5)]

## <a name="see-also"></a>Confira também
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: redimensionar controles de indicador](../vsto/how-to-resize-bookmark-controls.md)
