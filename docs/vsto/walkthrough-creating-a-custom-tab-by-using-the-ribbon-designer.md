---
title: 'Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], controlling from Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon Designer [Office development in Visual Studio]
- customizing the Ribbon, tabs
- custom Ribbon, tabs
- Custom tab [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a0089880e143c3db8f260141d9936058bf35b1ce
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38808866"
---
# <a name="walkthrough-create-a-custom-tab-by-using-the-ribbon-designer"></a>Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções
  Usando o Designer de faixa de opções, você pode criar uma guia personalizada e, em seguida, adicionar e posicionar controles nela.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   [Criar painéis de ações](#BKMK_CreateActionsPanes).  
  
-   [Criar uma guia personalizada](#BKMK_CreateCustomTab).  
  
-   [Ocultar e mostrar os painéis de ações usando os botões da guia personalizada](#BKMK_HideShowActionsPane).  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Excel  
  
## <a name="create-an-excel-workbook-project"></a>Criar um projeto de pasta de trabalho do Excel  
 As etapas para usar o Designer de faixa de opções são quase idênticas para todos os aplicativos do Office. Este exemplo usa uma pasta de trabalho do Excel.  
  
### <a name="to-create-an-excel-workbook-project"></a>Para criar um projeto de pasta de trabalho do Excel  
  
-   Criar um projeto de pasta de trabalho do Excel com o nome **MyExcelRibbon**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho no designer e adiciona o **MyExcelRibbon** projeto ao **Gerenciador de soluções**.  
  
##  <a name="BKMK_CreateActionsPanes"></a> Criar painéis de ações  
 Adicione dois painéis de ações personalizadas ao projeto. Posteriormente, você adicionará botões que mostrem e ocultem esses painéis de ações para a guia personalizada.  
  
### <a name="to-create-actions-panes"></a>Para criar painéis de ações  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **ActionsPaneControl**e, em seguida, escolha **adicionar**.  
  
     O **ActionsPaneControl1.cs** ou **ActionsPaneControl1.vb** arquivo é aberto no designer.  
  
3.  Dos **controles comuns** guia da **caixa de ferramentas**, adicione um rótulo à superfície do designer.  
  
4.  No **propriedades** janela, defina as **texto** propriedade de label1 a **painel de ações 1**.  
  
5.  Repita as etapas 1 a 5 para criar um segundo painel de ações e um rótulo. Defina as **texto** propriedade do segundo rótulo para **painel de ações 2**.  
  
##  <a name="BKMK_CreateCustomTab"></a> Criar uma guia personalizada  
 Uma das diretrizes de design de aplicativo do Office é que os usuários sempre devem ter o controle de interface do usuário do aplicativo do Office. Para adicionar esse recurso para os painéis de ações, você pode adicionar botões que mostrem e ocultem cada painel de ações de uma guia personalizada na faixa de opções. Para criar uma guia personalizada, adicione uma **faixa de opções (Visual Designer)** item ao projeto. O designer ajuda a adicionar e posicionar controles, definir propriedades de controles e manipular eventos de controle.  
  
### <a name="to-create-a-custom-tab"></a>Para criar uma guia personalizada  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **faixa de opções (Visual Designer)**.  
  
3.  Altere o nome da nova faixa de opções para **MyRibbon**e escolha **Add**.  
  
     O **MyRibbon.cs** ou **Myribbon** arquivo é aberto no Designer de faixa de opções e exibe um guia padrão e um grupo.  
  
4.  No Designer de faixa de opções, escolha a guia padrão.  
  
5.  No **propriedades** janela, expanda o **ControlId** propriedade e, em seguida, defina a **ControlIdType** propriedade **personalizado**.  
  
6.  Defina as **rótulo** propriedade **minha guia personalizada**.  
  
7.  No Designer de faixa de opções, escolha **group1**.  
  
8.  No **propriedades** janela, defina **rótulo** para **Gerenciador do painel Ações**.  
  
9. Dos **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste um botão para **group1**.  
  
10. Selecione **button1**.  
  
11. No **propriedades** janela, defina **rótulo** para **Mostrar painel de ações 1**.  
  
12. Adicione um segundo botão para **group1**e defina as **rótulo** propriedade a ser **Mostrar painel de ações 2**.  
  
13. Dos **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste uma **ToggleButton** controle para **group1**.  
  
14. Defina a **rótulo** propriedade **ocultar painel de ações**.  
  
##  <a name="BKMK_HideShowActionsPane"></a> Ocultar e mostrar os painéis de ações usando os botões da guia personalizada  
 A última etapa é adicionar código que responde ao usuário. Adicionar manipuladores de eventos para o <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> eventos dos dois botões e o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. Adicione código para esses manipuladores de eventos para permitir ocultar e mostrar os painéis de ações.  
  
### <a name="to-hide-and-show-actions-panes-by-using-buttons-in-the-custom-tab"></a>Para ocultar e mostrar os painéis de ações usando os botões na guia personalizada  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho *MyRibbon.cs* ou *Myribbon*e, em seguida, escolha **Exibir código**.  
  
2.  Adicione o seguinte código na parte superior do `MyRibbon` classe. Esse código cria dois objetos do painel Ações.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#1)]  
  
3.  Substitua o `MyRibbon_Load` método com o código a seguir. Esse código adiciona os objetos do painel de ações para o <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> coleta e oculta os objetos da exibição. O código do Visual c# também anexa delegados a vários eventos de controle de faixa de opções.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab#2](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#2)]
     [!code-vb[Trin_Ribbon_Custom_Tab#2](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#2)]  
  
4.  Adicione os seguintes métodos de manipulador de eventos de três para o `MyRibbon` classe. Esses métodos lidam com o <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> eventos dos dois botões e o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. Os manipuladores de eventos para button1 e button2 mostram painéis de ações alternativas. O manipulador de eventos para toggleButton1 mostra e oculta o painel de ações ativo.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab#3](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#3)]
     [!code-vb[Trin_Ribbon_Custom_Tab#3](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#3)]  
  
## <a name="test-the-custom-tab"></a>Testar a guia personalizada  
 Quando você executa o projeto, o Excel é iniciado e o **minha guia personalizada** guia é exibida na faixa de opções. Escolha os botões em **minha guia personalizada** para mostrar e ocultar os painéis de ações.  
  
### <a name="to-test-the-custom-tab"></a>Para testar a guia personalizada  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Escolha o **minha guia personalizada** guia.  
  
3.  No **Gerenciador do painel de ações personalizadas** grupo, escolha **Mostrar painel de ações 1**.  
  
     O painel de ações aparece e exibe o rótulo **painel de ações 1**.  
  
4.  Escolher **Mostrar painel de ações 2**.  
  
     O painel de ações aparece e exibe o rótulo **painel de ações 2**.  
  
5.  Escolher **ocultar painel de ações**.  
  
     Os painéis de ações não são mais visíveis.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como personalizar a interface do usuário do Office nesses tópicos:  
  
-   Adicione com base no contexto da interface do usuário para qualquer personalização de nível de documento. Para obter mais informações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md).  
  
-   Estenda um formulário personalizado ou padrão do Microsoft Office Outlook. Para obter mais informações, consulte [instruções passo a passo: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [Personalizar uma faixa de opções do Outlook](../vsto/customizing-a-ribbon-for-outlook.md)   
 [Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)   
 [Como: alterar a posição de uma guia na faixa de opções](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)   
 [Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)   
 [Como: adicionar controles ao modo de exibição backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)   
 [Visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md)  
  
  