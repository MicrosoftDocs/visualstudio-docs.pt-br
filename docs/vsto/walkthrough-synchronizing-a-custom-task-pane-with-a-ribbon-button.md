---
title: Sincronizar o painel de tarefas personalizado com o botão faixa de das
description: Saiba como você pode criar um painel de tarefas personalizado que os usuários podem ocultar ou exibir clicando em um botão de alternância na faixa de opção.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5e7fe64d2df3298d53f567d11fe765280843e2ce
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826779"
---
# <a name="walkthrough-synchronize-a-custom-task-pane-with-a-ribbon-button"></a>Walkthrough: sincronizar um painel de tarefas personalizado com um botão da faixa de das
  Este tutorial demonstra como criar um painel de tarefas personalizado que os usuários podem ocultar ou exibir clicando em um botão de alternância na faixa de opção. Você sempre deve criar um elemento de interface do usuário (IU), como um botão, que os usuários possam clicar para exibir ou ocultar seu painel de tarefas personalizado, pois os aplicativos Microsoft Office não fornecem uma maneira padrão para os usuários mostrarem ou ocultarem painéis de tarefas personalizados.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 Embora este passo a passos use o Excel especificamente, os conceitos demonstrados por instruções são aplicáveis a todos os aplicativos listados acima.

 Este passo a passo ilustra as seguintes tarefas:

- Criando a interface do usuário do painel de tarefas personalizado.

- Adicionando um botão de alternância à faixa de opção.

- Sincronizando o botão de alternância com o painel de tarefas personalizado.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel ou Microsoft [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] .

## <a name="create-the-add-in-project"></a>Criar o projeto de suplemento
 Nesta etapa, você criará um projeto de suplemento do VSTO para Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de suplemento do Excel com o nome **SynchronizeTaskPaneAndRibbon**, usando o modelo de projeto de suplemento do Excel. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo de código **ThisAddIn. cs** ou **ThisAddIn. vb** e adiciona o projeto **SynchronizeTaskPaneAndRibbon** ao **Gerenciador de soluções**.

## <a name="add-a-toggle-button-to-the-ribbon"></a>Adicionar um botão de alternância à faixa de opção
 Uma das diretrizes de design de aplicativos do Office é que os usuários sempre devem ter o controle da interface do usuário do aplicativo do Office. Para permitir que os usuários controlem o painel de tarefas personalizado, você pode adicionar um botão de alternância da faixa de opção que mostra e oculta o painel de tarefas. Para criar um botão de alternância, adicione um item **da faixa de opção (designer visual)** ao projeto. O designer ajuda você a adicionar e posicionar controles, definir propriedades de controle e manipular eventos de controle. Para obter mais informações, consulte [Designer de faixa](../vsto/ribbon-designer.md)de das.

### <a name="to-add-a-toggle-button-to-the-ribbon"></a>Para adicionar um botão de alternância à faixa de opção

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)**.

3. Altere o nome da nova faixa de forma para **ManageTaskPaneRibbon** e clique em **Adicionar**.

     O arquivo **ManageTaskPaneRibbon. cs** ou **ManageTaskPaneRibbon. vb** é aberto no designer de faixa de faixas e exibe uma guia e um grupo padrão.

4. No designer de faixa de faixas, clique em **grupo1**.

5. Na janela **Propriedades** , defina a propriedade **rótulo** como **Gerenciador de painéis de tarefas**.

6. Na guia **controles da faixa** de **ferramentas** do Office, arraste um **ToggleButton** para o grupo **Gerenciador de painéis de tarefas** .

7. Clique em **toggleButton1**.

8. Na janela **Propriedades** , defina a propriedade **rótulo** para **mostrar o painel de tarefas**.

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Criar a interface do usuário do painel de tarefas personalizado
 Não há nenhum designer visual para painéis de tarefas personalizados, mas você pode criar um controle de usuário com o layout desejado. Mais adiante neste tutorial, você adicionará o controle de usuário ao painel de tarefas personalizado.

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Para criar a interface do usuário do painel de tarefas personalizado

1. No menu **projeto** , clique em **Adicionar controle de usuário**.

2. Na caixa de diálogo **Adicionar novo item** , altere o nome do controle de usuário para **TaskPaneControl** e clique em **Adicionar**.

     O controle de usuário é aberto no designer.

3. Na guia **controles comuns** da caixa de **ferramentas**, arraste um controle **TextBox** para o controle de usuário.

## <a name="create-the-custom-task-pane"></a>Criar o painel de tarefas personalizado
 Para criar o painel de tarefas personalizado quando o suplemento do VSTO for iniciado, adicione o controle de usuário ao painel de tarefas no <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos do suplemento do VSTO. Por padrão, o painel de tarefas personalizado não será visível. Mais adiante neste tutorial, você adicionará o código que exibirá ou ocultará o painel de tarefas quando o usuário clicar no botão de alternância que você adicionou à faixa de opção.

### <a name="to-create-the-custom-task-pane"></a>Para criar o painel de tarefas personalizado

1. Em **Gerenciador de soluções**, expanda **Excel**.

2. Clique com o botão direito do mouse em **ThisAddIn. cs** ou em **ThisAddIn. vb** e clique em **Exibir código**.

3. Adicione o código a seguir à classe `ThisAddIn` . Esse código declara uma instância do `TaskPaneControl` como um membro de `ThisAddIn` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet1":::

4. Substitua o `ThisAddIn_Startup` manipulador de eventos pelo código a seguir. Esse código adiciona o `TaskPaneControl` objeto ao `CustomTaskPanes` campo, mas não exibe o painel de tarefas personalizado (por padrão, a <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> propriedade da <xref:Microsoft.Office.Tools.CustomTaskPane> classe é **false**). O código do Visual C# também anexa um manipulador de eventos ao <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> evento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet2":::

5. Adicione o método a seguir à classe `ThisAddIn`. Esse método manipula o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> evento. Quando o usuário fecha o painel de tarefas clicando no botão **fechar** (X), esse método atualiza o estado do botão de alternância na faixa de opção.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet3":::

6. Adicione a propriedade a seguir à `ThisAddIn` classe. Essa propriedade expõe o `myCustomTaskPane1` objeto particular para outras classes. Mais adiante neste tutorial, você adicionará o código à `MyRibbon` classe que usa essa propriedade.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet4":::

## <a name="hide-and-show-the-custom-task-pane-by-using-the-toggle-button"></a>Ocultar e mostrar o painel de tarefas personalizado usando o botão de alternância
 A última etapa é adicionar o código que exibe ou oculta o painel de tarefas personalizado quando o usuário clica no botão de alternância na faixa de opção.

### <a name="to-display-and-hide-the-custom-task-pane-by-using-the-toggle-button"></a>Para exibir e ocultar o painel de tarefas personalizado usando o botão de alternância

1. No designer de faixa de opção, clique duas vezes no botão de alternância **Mostrar painel de tarefas** .

     O Visual Studio gera automaticamente um manipulador de eventos chamado `toggleButton1_Click` , que manipula o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. O Visual Studio também abre o arquivo *MyRibbon. cs* ou *MyRibbon. vb* no editor de código.

2. Substitua o `toggleButton1_Click` manipulador de eventos pelo código a seguir. Quando o usuário clica no botão de alternância, esse código exibe ou oculta o painel de tarefas personalizado, dependendo se o botão de alternância é pressionado ou não pressionado.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.cs" id="Snippet5":::

## <a name="test-the-add-in"></a>Testar o suplemento
 Quando você executa o projeto, o Excel é aberto sem exibir o painel de tarefas personalizado. Clique no botão de alternância na faixa de opção para testar o código.

### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5** para executar o projeto.

     Confirme se o Excel é aberto e se a guia suplementos aparece na faixa de **bits** .

2. Clique na guia suplementos na faixa de **bits** .

3. No grupo **Gerenciador de painéis de tarefas** , clique no botão de alternância **Mostrar painel de tarefas** .

     Verifique se o painel de tarefas é exibido de forma alternativa e oculto quando você clica no botão de alternância.

4. Quando o painel de tarefas estiver visível, clique no botão **fechar** (X) no canto do painel de tarefas.

     Verifique se o botão de alternância parece não ser pressionado.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar painéis de tarefas personalizados a partir destes tópicos:

- Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

- Automatize um aplicativo de um painel de tarefas personalizado. Para obter mais informações, consulte [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md).

- Crie um painel de tarefas personalizado para cada mensagem de email aberta no Outlook. Para obter mais informações, consulte [Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md).

## <a name="see-also"></a>Consulte também
- [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)
- [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
