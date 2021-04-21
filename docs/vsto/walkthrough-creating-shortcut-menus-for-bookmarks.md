---
title: 'Walkthrough: criar menus de atalho para indicadores'
description: Saiba como criar menus de atalho para controles de indicadores em uma personalização em nível de documento para o Microsoft Word.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 48381d452b0c67a34581092a47896aba60e7125c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826298"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>Walkthrough: criar menus de atalho para indicadores
  Este tutorial demonstra como criar menus de atalho para <xref:Microsoft.Office.Tools.Word.Bookmark> controles em uma personalização em nível de documento para o Word. Quando um usuário clica com o botão direito do mouse no texto em um indicador, um menu de atalho é exibido e fornece ao usuário as opções para formatar o texto.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- [Crie o projeto](#BKMK_CreateProject).

- [Adicione texto e indicadores ao documento](#BKMK_addtextandbookmarks).

- [Adicione comandos a um menu de atalho](#BKMK_AddCmndsShortMenu).

- [Formate o texto no indicador](#BKMK_formattextbkmk).

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="create-the-project"></a><a name="BKMK_CreateProject"></a> Criar o projeto
 A primeira etapa é criar um projeto de documento do Word no Visual Studio.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

- Crie um projeto de documento do Word que tenha o nome **meu menu de atalho de indicador**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o novo documento do Word no designer e adiciona o projeto de **menu de atalho meu favorito** a **Gerenciador de soluções**.

## <a name="add-text-and-bookmarks-to-the-document"></a><a name="BKMK_addtextandbookmarks"></a> Adicionar texto e indicadores ao documento
 Adicione texto ao documento e, em seguida, adicione dois indicadores sobrepostos.

### <a name="to-add-text-to-your-document"></a>Para adicionar texto ao documento

- No documento que aparece no designer do seu projeto, digite o texto a seguir.

     **Este é um exemplo de criação de um menu de atalho quando você clica com o botão direito do mouse no texto de um indicador.**

### <a name="to-add-a-bookmark-control-to-your-document"></a>Para adicionar um controle de indicador ao documento

1. Na **caixa de ferramentas**, na guia **controles do Word** , arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o documento.

    A caixa de diálogo **Adicionar controle de indicadores** é exibida.

2. Selecione as palavras "criando um menu de atalho ao clicar com o botão direito do mouse no texto" e, em seguida, clique em **OK**.

    `bookmark1` é adicionado ao documento.

3. Adicione outro <xref:Microsoft.Office.Tools.Word.Bookmark> controle às palavras "clique com o botão direito do mouse no texto em um indicador".

    `bookmark2` é adicionado ao documento.

   > [!NOTE]
   > As palavras "clique com o botão direito do mouse no texto" estão no `bookmark1` e no `bookmark2` .

   Quando você adiciona um indicador a um documento em tempo de design, um <xref:Microsoft.Office.Tools.Word.Bookmark> controle é criado. Você pode programar em vários eventos do indicador. Você pode escrever código no <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> evento do indicador para que, quando o usuário clicar com o botão direito do mouse no texto do indicador, um menu de atalho seja exibido.

## <a name="add-commands-to-a-shortcut-menu"></a><a name="BKMK_AddCmndsShortMenu"></a> Adicionar comandos a um menu de atalho
 Adicione botões ao menu de atalho que aparece quando você clica com o botão direito do mouse no documento.

### <a name="to-add-commands-to-a-shortcut-menu"></a>Para adicionar comandos a um menu de atalho

1. Adicione um item **XML da faixa de faixas** ao projeto. Para obter mais informações, consulte [como: começar a personalizar a faixa de](../vsto/how-to-get-started-customizing-the-ribbon.md)visualização.

2. Em **Gerenciador de soluções**, selecione **ThisDocument. cs** ou **ThisDocument. vb**.

3. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo de classe **ThisDocument** é aberto no editor de código.

4. Adicione o código a seguir à classe **ThisDocument** . Esse código substitui o método CreateRibbonExtensibilityObject e retorna a classe XML da faixa de forma para o aplicativo do Office.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet1":::

5. Em **Gerenciador de soluções**, selecione o arquivo XML da faixa de opções. Por padrão, o arquivo XML da faixa de faixas é denominado Ribbon1.xml.

6. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo XML da faixa de faixas é aberto no editor de códigos.

7. No editor de código, substitua o conteúdo do arquivo XML da faixa de opções pelo código a seguir.

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui" onLoad="Ribbon_Load">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="BoldButton" label="Bold" onAction="ButtonClick"
               getVisible="GetVisible" />
          <button id="ItalicButton" label="Italic" onAction="ButtonClick"
              getVisible="GetVisible"/>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

     Esse código adiciona dois botões ao menu de atalho que aparece quando você clica com o botão direito do mouse no documento.

8. No **Gerenciador de soluções**, clique com o botão direito do mouse em `ThisDocument` e clique em **Exibir código**.

9. Declare as variáveis a seguir e uma variável de indicador no nível de classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet2":::

10. Em **Gerenciador de soluções**, selecione o arquivo de código da faixa de opções. Por padrão, o arquivo de código da faixa de faixas é denominado **Ribbon1. cs** ou **Ribbon1. vb**.

11. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo de código da faixa de Ribbon é aberto no editor de código.

12. No arquivo de código da faixa de opções, adicione o método a seguir. Esse é um método de retorno de chamada para os dois botões que você adicionou ao menu de atalho do documento. Esse método determina se esses botões aparecem no menu de atalho. Os botões negrito e itálico serão exibidos apenas se você clicar com o botão direito do mouse no texto dentro do indicador.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet5":::

## <a name="format-the-text-in-the-bookmark"></a><a name="BKMK_formattextbkmk"></a> Formatar o texto no indicador

### <a name="to-format-the-text-in-the-bookmark"></a>Para formatar o texto no indicador

1. No arquivo de código da faixa de opções, adicione um `ButtonClick` manipulador de eventos para aplicar formatação ao indicador.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet6":::

2. **Gerenciador de soluções**, selecione **ThisDocument. cs** ou **ThisDocument. vb**.

3. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo de classe **ThisDocument** é aberto no editor de código.

4. Adicione o código a seguir à classe **ThisDocument** .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet3":::

    > [!NOTE]
    > Você deve escrever o código para lidar com o caso em que os indicadores se sobrepõem. Se você não fizer isso, por padrão, o código será chamado para todos os indicadores na seleção.

5. No C#, você deve adicionar manipuladores de eventos para os controles de indicador ao <xref:Microsoft.Office.Tools.Word.Document.Startup> evento. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet4":::

## <a name="test-the-application"></a>Testar o aplicativo
 Teste seu documento para verificar se os itens de menu em negrito e itálico aparecem no menu de atalho quando você clica com o botão direito do mouse em texto em um indicador e se o texto está formatado corretamente.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Clique com o botão direito do mouse no primeiro indicador e clique em **negrito**.

3. Verifique se todo o texto em `bookmark1` está formatado como negrito.

4. Clique com o botão direito do mouse no texto em que os indicadores se sobrepõem e clique em **itálico**.

5. Verifique se todo o texto em `bookmark2` está em itálico e somente a parte do texto `bookmark1` que se sobrepõe `bookmark2` é itálico.

## <a name="next-steps"></a>Próximas etapas
 Estas são algumas tarefas que podem vir a seguir:

- Escreva o código para responder a eventos de controles de host no Excel. Para obter mais informações, consulte [Walkthrough: programa em relação a eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md).

- Use uma caixa de seleção para alterar a formatação em um indicador. Para obter mais informações, consulte [Walkthrough: alterar a formatação do documento usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md).

## <a name="see-also"></a>Consulte também
- [Passo a passos usando o Word](../vsto/walkthroughs-using-word.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Controle de indicador](../vsto/bookmark-control.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
