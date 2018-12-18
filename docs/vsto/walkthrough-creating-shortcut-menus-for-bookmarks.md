---
title: 'Passo a passo: Criar menus de atalho para indicadores'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ff261fd6032f3c666dfa3d745508586ffede6504
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884076"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>Passo a passo: Criar menus de atalho para indicadores
  Este passo a passo demonstra como criar menus de atalho para <xref:Microsoft.Office.Tools.Word.Bookmark> controles em uma personalização no nível de documento para Word. Quando um usuário clica o texto em um indicador, um menu de atalho é exibido e fornece as opções de usuário para formatar o texto.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- [Criar o projeto](#BKMK_CreateProject).  
  
- [Adicionar texto e indicadores no documento](#BKMK_addtextandbookmarks).  
  
- [Adicionar comandos ao menu de atalho](#BKMK_AddCmndsShortMenu).  
  
- [Formatar o texto no indicador](#BKMK_formattextbkmk).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]  
  
##  <a name="BKMK_CreateProject"></a> Criar o projeto  
 A primeira etapa é criar um projeto de documento do Word no Visual Studio.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
-   Criar um projeto de documento do Word que tem o nome **meu Menu de atalho do indicador**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre o novo documento do Word no designer e adiciona o **meu Menu de atalho do indicador** projeto ao **Gerenciador de soluções**.  
  
##  <a name="BKMK_addtextandbookmarks"></a> Adicionar texto e indicadores no documento  
 Adicionar algum texto ao documento e, em seguida, adicione dois indicadores sobrepostos.  
  
### <a name="to-add-text-to-your-document"></a>Para adicionar texto ao documento  
  
-   No documento que aparece no designer do seu projeto, digite o texto a seguir.  
  
     **Este é um exemplo de criação de um menu de atalho quando o botão direito do mouse o texto em um indicador.**  
  
### <a name="to-add-a-bookmark-control-to-your-document"></a>Para adicionar um controle de indicador para o seu documento  
  
1. No **caixa de ferramentas**, da **controles do Word** guia, arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao documento.  
  
    O **adicionar controle de indicador** caixa de diálogo é exibida.  
  
2. Selecione as palavras "Criando um menu de atalho quando o botão direito do mouse o texto" e, em seguida, clique em **Okey**.  
  
    `bookmark1` é adicionado ao documento.  
  
3. Adicione outro <xref:Microsoft.Office.Tools.Word.Bookmark> o controle para as palavras "com o botão direito do texto em um indicador".  
  
    `bookmark2` é adicionado ao documento.  
  
   > [!NOTE]  
   >  As palavras "com o botão direito o texto" está em ambos os `bookmark1` e `bookmark2`.  
  
   Quando você adiciona um indicador a um documento em tempo de design, um <xref:Microsoft.Office.Tools.Word.Bookmark> controle é criado. Você pode programar vários eventos do indicador. Você pode escrever código no <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> evento do indicador, de modo que quando o usuário clica o texto no indicador, um menu de atalho é exibido.  
  
##  <a name="BKMK_AddCmndsShortMenu"></a> Adicionar comandos ao menu de atalho  
 Adicione botões ao menu de atalho que aparece quando o botão direito do mouse no documento.  
  
### <a name="to-add-commands-to-a-shortcut-menu"></a>Adicionar comandos ao menu de atalho  
  
1.  Adicionar um **XML da faixa de opções** item ao projeto. Para obter mais informações, consulte [como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md).  
  
2.  Na **Gerenciador de soluções**, selecione **ThisDocument.cs** ou **ThisDocument**.  
  
3.  Na barra de menus, escolha **Exibir** > **Código**.  
  
     O **ThisDocument** arquivo de classe é aberto no Editor de códigos.  
  
4.  Adicione o seguinte código para o **ThisDocument** classe. Esse código substitui o método CreateRibbonExtensibilityObject e retorna a classe XML da faixa de opções para o aplicativo do Office.  
  
     [!code-csharp[Trin_Word_Document_Menus#1](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#1)]
     [!code-vb[Trin_Word_Document_Menus#1](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#1)]  
  
5.  Na **Gerenciador de soluções**, selecione o arquivo XML de faixa de opções. Por padrão, o arquivo XML de faixa de opções é denominado Ribbon1.xml.  
  
6.  Na barra de menus, escolha **Exibir** > **Código**.  
  
     O arquivo xml de faixa de opções é aberto no Editor de códigos.  
  
7.  No Editor de códigos, substitua o conteúdo do arquivo XML de faixa de opções com o código a seguir.  
  
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
  
     Esse código adiciona dois botões ao menu de atalho que aparece quando o botão direito do mouse no documento.  
  
8.  Na **Gerenciador de soluções**, clique com botão direito `ThisDocument`e, em seguida, clique em **Exibir código**.  
  
9. Declare as variáveis a seguir e uma variável de indicador no nível de classe.  
  
     [!code-csharp[Trin_Word_Document_Menus#2](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#2)]
     [!code-vb[Trin_Word_Document_Menus#2](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#2)]  
  
10. Na **Gerenciador de soluções**, selecione o arquivo de código da faixa de opções. Por padrão, o arquivo de código da faixa de opções é denominado **Ribbon1.cs** ou **Ribbon1.vb**.  
  
11. Na barra de menus, escolha **Exibir** > **Código**.  
  
     O arquivo de código da faixa de opções é aberto no Editor de códigos.  
  
12. No arquivo de código da faixa de opções, adicione o seguinte método. Esse é um método de retorno de chamada para os dois botões que você adicionou ao menu de atalho do documento. Este método determina se esses botões são exibidos no menu de atalho. Os botões de negrito e itálico aparecem somente se o botão direito do mouse texto dentro do indicador.  
  
     [!code-csharp[Trin_Word_Document_Menus#5](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#5)]
     [!code-vb[Trin_Word_Document_Menus#5](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#5)]  
  
##  <a name="BKMK_formattextbkmk"></a> Formatar o texto no indicador  
  
### <a name="to-format-the-text-in-the-bookmark"></a>Para formatar o texto no indicador  
  
1.  No arquivo de código da faixa de opções, adicione um `ButtonClick` manipulador de eventos para aplicar formatação ao indicador.  
  
     [!code-csharp[Trin_Word_Document_Menus#6](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs#6)]
     [!code-vb[Trin_Word_Document_Menus#6](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb#6)]  
  
2.  **Gerenciador de soluções**, selecione **ThisDocument.cs** ou **ThisDocument**.  
  
3.  Na barra de menus, escolha **Exibir** > **Código**.  
  
     O **ThisDocument** arquivo de classe é aberto no Editor de códigos.  
  
4.  Adicione o seguinte código para o **ThisDocument** classe.  
  
     [!code-csharp[Trin_Word_Document_Menus#3](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#3)]
     [!code-vb[Trin_Word_Document_Menus#3](../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb#3)]  
  
    > [!NOTE]  
    >  Você deve escrever código para manipular o caso em que os indicadores se sobrepõem. Se você não fizer isso, por padrão, o código será chamado para todos os indicadores na seleção.  
  
5.  No c#, você deve adicionar manipuladores de eventos para os controles de indicador para o <xref:Microsoft.Office.Tools.Word.Document.Startup> eventos. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_Word_Document_Menus#4](../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs#4)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Teste seu documento para verificar se os itens de menu em negrito e itálico aparecem no menu de atalho quando o botão direito do mouse texto em um indicador e o texto está formatado corretamente.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Clique com botão direito no primeiro indicador e, em seguida, clique em **negrito**.  
  
3.  Verifique se que todo o texto em `bookmark1` é formatado como negrito.  
  
4.  O texto em que os indicadores se sobrepõem, com o botão direito e, em seguida, clique em **itálico**.  
  
5.  Verifique se que todo o texto no `bookmark2` é itálico e somente a parte do texto na `bookmark1` que se sobrepõe `bookmark2` está em itálico.  
  
## <a name="next-steps"></a>Próximas etapas  
 Estas são algumas tarefas que podem vir a seguir:  
  
-   Escreva código para responder a eventos de controles de host no Excel. Para obter mais informações, consulte [instruções passo a passo: programa contra eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md).  
  
-   Use uma caixa de seleção para alterar a formatação em um indicador. Para obter mais informações, consulte [instruções passo a passo: formatação de documento de alteração usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo usando o Word](../vsto/walkthroughs-using-word.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controle de indicador](../vsto/bookmark-control.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  