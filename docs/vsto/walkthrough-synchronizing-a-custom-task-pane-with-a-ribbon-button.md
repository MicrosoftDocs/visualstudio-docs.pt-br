---
title: 'Passo a passo: Sincronizar um painel de tarefas personalizado com um botão da faixa de opções'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom task panes [Office development in Visual Studio], showing and hiding
- showing custom task panes
- Ribbon [Office development in Visual Studio], custom task panes
- toggle buttons [Office development in Visual Studio]
- custom task panes [Office development in Visual Studio], synchronizing with Ribbon button
- user interfaces [Office development in Visual Studio], custom task panes
- synchronization [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], showing and hiding
- custom task panes [Office development in Visual Studio], creating
- hiding custom task panes
- task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio], synchronizing with Ribbon button
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7b6c36e93d9dd8dd4ef81d0d124ae33e842a16d7
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670092"
---
# <a name="walkthrough-synchronize-a-custom-task-pane-with-a-ribbon-button"></a>Passo a passo: Sincronizar um painel de tarefas personalizado com um botão da faixa de opções
  Este passo a passo demonstra como criar um painel de tarefas personalizado que os usuários podem ocultar ou exibir clicando em um botão de alternância na faixa de opções. Você sempre deve criar um elemento de interface do usuário do usuário, como um botão, o que os usuários podem clicar para exibir ou ocultar o painel de tarefas, porque os aplicativos do Microsoft Office não fornecem uma maneira padrão para os usuários mostrar ou ocultar painéis de tarefas personalizados.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Embora este passo a passo usa o Excel especificamente, os conceitos demonstrados pelo passo a passo são aplicáveis a todos os aplicativos que estão listados acima.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Projetando a interface do usuário do painel de tarefas personalizado.  
  
-   Adicionando um botão de alternância para a faixa de opções.  
  
-   Sincronizando o botão de alternância com o painel de tarefas personalizado.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   O Microsoft Excel ou Microsoft [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)].  
  
## <a name="create-the-add-in-project"></a>Criar o projeto de suplemento  
 Nesta etapa, você criará um projeto de suplemento do VSTO para Excel.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de suplemento do Excel com o nome **SynchronizeTaskPaneAndRibbon**, usando o modelo de projeto do suplemento do Excel. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **ThisAddIn.cs** ou **ThisAddIn. vb** arquivo de código e adiciona os **SynchronizeTaskPaneAndRibbon** projeto ao **Solution Explorer**.  
  
## <a name="add-a-toggle-button-to-the-ribbon"></a>Adicionar um botão de alternância para a faixa de opções  
 Uma das diretrizes de design de aplicativo do Office é que os usuários sempre devem ter o controle de interface do usuário do aplicativo do Office. Para habilitar usuários controlar o painel de tarefas personalizado, você pode adicionar um botão de alternância de faixa de opções que mostra e oculta o painel de tarefas. Para criar um botão de alternância, adicione uma **faixa de opções (Visual Designer)** item ao projeto. O designer ajuda a adicionar e posicionar controles, definir propriedades de controles e manipular eventos de controle. Para obter mais informações, consulte [designer de faixa de opções](../vsto/ribbon-designer.md).  
  
### <a name="to-add-a-toggle-button-to-the-ribbon"></a>Para adicionar um botão de alternância para a faixa de opções  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **faixa de opções (Visual Designer)**.  
  
3.  Altere o nome da nova faixa de opções para **ManageTaskPaneRibbon**e clique em **Add**.  
  
     O **ManageTaskPaneRibbon.cs** ou **ManageTaskPaneRibbon.vb** arquivo é aberto no Designer de faixa de opções e exibe um guia padrão e um grupo.  
  
4.  No Designer de faixa de opções, clique em **group1**.  
  
5.  No **propriedades** janela, defina as **rótulo** propriedade a ser **Gerenciador de tarefas do painel**.  
  
6.  Do **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste uma **ToggleButton** para o **Gerenciador de tarefas do painel** grupo.  
  
7.  Clique em **toggleButton1**.  
  
8.  No **propriedades** janela, defina as **rótulo** propriedade a ser **Mostrar painel de tarefas**.  
  
## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Projetar a interface do usuário do painel de tarefas personalizado  
 Não há nenhum designer visual para painéis de tarefas personalizados, mas você pode criar um controle de usuário com o layout desejado. Posteriormente neste passo a passo, você irá adicionar o controle de usuário para o painel de tarefas personalizado.  
  
### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Ao projetar a interface do usuário do painel de tarefas personalizado  
  
1.  Sobre o **Project** menu, clique em **adicionar controle de usuário**.  
  
2.  No **Adicionar Novo Item** diálogo caixa, altere o nome do controle de usuário para **TaskPaneControl**e clique em **adicionar**.  
  
     O controle de usuário é aberto no designer.  
  
3.  Dos **controles comuns** guia da **caixa de ferramentas**, arraste uma **caixa de texto** controle para o controle de usuário.  
  
## <a name="create-the-custom-task-pane"></a>Criar o painel de tarefas personalizado  
 Para criar o painel de tarefas personalizado quando o suplemento do VSTO é iniciado, adicione o controle de usuário ao painel de tarefas no <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos do que o suplemento do VSTO. Por padrão, o painel de tarefas personalizado não será visível. Posteriormente neste passo a passo, você irá adicionar código que irá exibir ou ocultar o painel de tarefas quando o usuário clica no botão de alternância que você adicionou à faixa de opções.  
  
### <a name="to-create-the-custom-task-pane"></a>Para criar o painel de tarefas personalizado  
  
1.  Na **Gerenciador de soluções**, expanda **Excel**.  
  
2.  Clique com botão direito **ThisAddIn.cs** ou **ThisAddIn. vb** e clique em **Exibir código**.  
  
3.  Adicione o seguinte código para o `ThisAddIn` classe. Esse código declara uma instância de `TaskPaneControl` como um membro de `ThisAddIn`.  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#1)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#1)]  
  
4.  Substitua o `ThisAddIn_Startup` manipulador de eventos com o código a seguir. Esse código adiciona o `TaskPaneControl` do objeto para o `CustomTaskPanes` campo, mas ele não exibe o painel de tarefas personalizado (por padrão, o <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> propriedade do <xref:Microsoft.Office.Tools.CustomTaskPane> classe é **false**). O código do Visual c# também anexa um manipulador de eventos para o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> eventos.  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#2)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#2)]  
  
5.  Adicione o seguinte método à classe `ThisAddIn`. Este método trata o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> eventos. Quando o usuário fechar o painel de tarefas clicando o **fechar** botão (X), essas atualizações de método, o estado de alternância botão na faixa de opções.  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#3)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#3)]  
  
6.  Adicione a seguinte propriedade para o `ThisAddIn` classe. Essa propriedade expõe particular `myCustomTaskPane1` objeto a outras classes. Posteriormente neste passo a passo, você adicionará código para o `MyRibbon` classe que usa essa propriedade.  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#4)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#4)]  
  
## <a name="hide-and-show-the-custom-task-pane-by-using-the-toggle-button"></a>Ocultar e mostrar o painel de tarefas personalizados usando o botão de alternância  
 A última etapa é adicionar código que exibe ou oculta o painel de tarefas personalizado quando o usuário clica no botão de alternância na faixa de opções.  
  
### <a name="to-display-and-hide-the-custom-task-pane-by-using-the-toggle-button"></a>Para exibir e ocultar o painel de tarefas personalizados usando o botão de alternância  
  
1.  No Designer de faixa de opções, clique duas vezes o **Mostrar painel de tarefas** botão de alternância.  
  
     Visual Studio gera automaticamente um manipulador de eventos chamado `toggleButton1_Click`, que trata o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. O Visual Studio também abre a *MyRibbon.cs* ou *Myribbon* arquivo no Editor de códigos.  
  
2.  Substitua o `toggleButton1_Click` manipulador de eventos com o código a seguir. Quando o usuário clica no botão de alternância, esse código exibe ou oculta o painel de tarefas personalizado, dependendo se o botão de alternância é pressionado ou não pressionado.  
  
     [!code-vb[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.vb#5)]
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.cs#5)]  
  
## <a name="test-the-add-in"></a>Testar o suplemento  
 Quando você executa o projeto, o Excel é aberto sem exibir o painel de tarefas personalizado. Clique no botão de alternância na faixa de opções para testar o código.  
  
### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1.  Pressione **F5** para executar o projeto.  
  
     Confirme que o Excel abrir e o **Add-Ins** guia é exibida na faixa de opções.  
  
2.  Clique o **Add-Ins** guia na faixa de opções.  
  
3.  No **Gerenciador de tarefas do painel** , clique no **Mostrar painel de tarefas** botão de alternância.  
  
     Verifique se o painel de tarefas é exibido e ocultado quando você clicar no botão de alternância como alternativa.  
  
4.  Quando o painel de tarefas estiver visível, clique no **fechar** botão (X) no canto do painel de tarefas.  
  
     Verifique se o botão de alternância aparece não seja pressionado.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como criar painéis de tarefas personalizados com estes tópicos:  
  
-   Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
-   Automatize um aplicativo de um painel de tarefas personalizado. Para obter mais informações, consulte [instruções passo a passo: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md).  
  
-   Crie um painel de tarefas personalizado para cada mensagem de email que é aberto no Outlook. Para obter mais informações, consulte [instruções passo a passo: exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md).  
  
## <a name="see-also"></a>Consulte também  
 [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)   
 [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)   
 [Passo a passo: Automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)   
 [Passo a passo: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)  
  
  