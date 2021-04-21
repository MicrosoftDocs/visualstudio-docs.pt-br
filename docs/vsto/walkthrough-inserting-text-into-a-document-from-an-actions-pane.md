---
title: 'Walkthrough: inserir texto em um documento a partir de um painel Ações'
description: Crie um painel Ações em um documento do Microsoft Word. Saiba que o painel Ações contém dois controles que coletam entrada e, em seguida, enviam o texto para o documento.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1ac42954e32b30a293abbe031218213948fb103a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824972"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>Walkthrough: inserir texto em um documento a partir de um painel Ações
  Este tutorial demonstra como criar um painel Ações em um Microsoft Office documento do Word. O painel Ações contém dois controles que coletam entrada e enviam o texto ao documento.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Crie uma interface usando controles de Windows Forms em um controle do painel Ações.

- Exibe o painel ações quando o aplicativo é aberto.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de Documento do Word.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de documento do Word com o nome **meu painel ações básicas**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o novo documento do Word no designer e adiciona o projeto do **painel minhas ações básicas** ao **Gerenciador de soluções**.

## <a name="add-text-and-bookmarks-to-the-document"></a>Adicionar texto e indicadores ao documento
 O painel Ações enviará texto para indicadores no documento. Para projetar o documento, digite algum texto para criar um formulário básico.

### <a name="to-add-text-to-your-document"></a>Para adicionar texto ao documento

1. Digite o seguinte texto em seu documento do Word:

    **21 de março de 2008**

    **Nome**

    **Endereço**

    **Este é um exemplo de um painel ações básicas no Word.**

   Você pode adicionar um <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao seu documento arrastando-o da caixa de **ferramentas** no Visual Studio ou usando o **marcador** de diálogo no Word.

### <a name="to-add-a-bookmark-control-to-your-document"></a>Para adicionar um controle de indicador ao documento

1. Na guia **controles do Word** da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o documento.

     A caixa de diálogo **Adicionar controle de indicadores** é exibida.

2. Selecione o **nome** da palavra, sem selecionar a marca de parágrafo e clique em **OK**.

    > [!NOTE]
    > A marca de parágrafo deve estar fora do indicador. Se as marcas de parágrafo não estiverem visíveis no documento, clique no menu **ferramentas** , aponte para **Microsoft Office ferramentas do Word** e clique em **Opções**. Clique na guia **Exibir** e marque a caixa de seleção **marcas de parágrafo** na seção marcas de **formatação** da caixa de diálogo **Opções** .

3. Na janela **Propriedades** , altere a propriedade **Name** de **Bookmark1** para **nome** do servidor.

4. Selecione o **endereço** da palavra, sem selecionar a marca de parágrafo.

5. Na guia **Inserir** da faixa de faixas, no grupo **links** , clique em **indicador**.

6. Na caixa de diálogo **indicador** , digite nome do **destinatário** na caixa **nome do indicador** e clique em **Adicionar**.

## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel Ações
 Para criar a interface do painel Ações, adicione um controle do painel Ações ao projeto e, em seguida, adicione Windows Forms controles ao controle do painel Ações.

### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações

1. Selecione o projeto do **painel minhas ações básicas** no **Gerenciador de soluções**.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , clique no **controle do painel Ações**, nomeie o controle **InsertTextControl** e clique em **Adicionar**.

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>Para adicionar controles de formulário do Windows ao controle do painel Ações

1. Se o controle do painel ações não estiver visível no designer, clique duas vezes em **InsertTextControl**.

2. Na guia **controles comuns** da caixa de **ferramentas**, arraste um controle **rótulo** para o controle do painel Ações.

3. Altere a propriedade **Text** do controle rótulo para **nome**.

4. Adicione um controle **TextBox** ao controle do painel Ações e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**getName**|
    |**Tamanho**|**130, 20**|

5. Adicione um segundo controle **rótulo** ao controle do painel Ações e altere a propriedade **texto** para **endereço**.

6. Adicione um segundo controle **TextBox** ao controle do painel Ações e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**GetAddress**|
    |**Aceita o retorno**|**True**|
    |**Multilinha**|**True**|
    |**Tamanho**|**130, 40**|

7. Adicione um controle de **botão** ao controle do painel Ações e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**addText**|
    |**Text**|**Inserção**|

## <a name="add-code-to-insert-text-into-the-document"></a>Adicionar código para inserir texto no documento
 No painel Ações, escreva o código que insere o texto das caixas de texto nos controles apropriados do <xref:Microsoft.Office.Tools.Word.Bookmark> documento. Você pode usar a `Globals` classe para acessar controles no documento a partir dos controles no painel Ações. Para obter mais informações, consulte [acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>Para inserir texto do painel Ações em um indicador no documento

1. Adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão **AddText** .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb" id="Snippet8":::

2. No C#, você deve adicionar um manipulador de eventos para o clique do botão. Você pode posicionar esse código no `InsertTextControl` Construtor após a chamada para `InitializeComponent` . Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet9":::

## <a name="add-code-to-show-the-actions-pane"></a>Adicionar código para mostrar o painel Ações
 Para mostrar o painel Ações, adicione o controle que você criou à coleção de controle.

### <a name="to-show-the-actions-pane"></a>Para mostrar o painel Ações

1. Crie uma nova instância do controle do painel Ações na `ThisDocument` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet10":::

2. Adicione o código a seguir ao <xref:Microsoft.Office.Tools.Word.Document.Startup> manipulador de eventos de `ThisDocument` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet11":::

## <a name="test-the-application"></a>Testar o aplicativo
 Teste seu documento para verificar se o painel Ações é aberto quando o documento é aberto e esse texto digitado nas caixas de texto é inserido nos indicadores quando o botão é clicado.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Confirme se o painel Ações está visível.

3. Digite seu nome e endereço nas caixas de texto no painel Ações e clique em **Inserir**.

## <a name="next-steps"></a>Próximas etapas
 Estas são algumas tarefas que podem vir a seguir:

- Crie um painel Ações no Excel. Para obter mais informações, consulte [como: adicionar um painel ações a pastas de trabalho do Excel](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100)).

- Associar dados a controles em um painel Ações. Para obter mais informações, consulte [Walkthrough: associar dados a controles em um painel de ações do Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md).

## <a name="see-also"></a>Consulte também
- [Visão geral do painel Ações](../vsto/actions-pane-overview.md)
- [Como: adicionar um painel de ações a documentos do Word ou a pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Como: adicionar um painel de ações a pastas de trabalho do Excel](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [Como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Controle de indicador](../vsto/bookmark-control.md)
