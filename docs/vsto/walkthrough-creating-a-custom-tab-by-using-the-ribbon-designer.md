---
title: 'Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas'
description: Saiba como você pode criar uma guia personalizada e, em seguida, adicionar e posicionar controles nela usando o designer de faixa de faixas.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3886e20d45834f98f36b8d7e48f3b11c9ef7d5dd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824814"
---
# <a name="walkthrough-create-a-custom-tab-by-using-the-ribbon-designer"></a>Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas
  Usando o designer de faixa de faixas, você pode criar uma guia personalizada e, em seguida, adicionar e posicionar controles nela.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- [Criar painéis de ações](#BKMK_CreateActionsPanes).

- [Crie uma guia personalizada](#BKMK_CreateCustomTab).

- [Oculte e mostre painéis de ações usando botões na guia personalizado](#BKMK_HideShowActionsPane).

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-an-excel-workbook-project"></a>Criar um projeto de pasta de trabalho do Excel
 As etapas para usar o designer de faixa de faixas são quase idênticas para todos os aplicativos do Office. Este exemplo usa uma pasta de trabalho do Excel.

### <a name="to-create-an-excel-workbook-project"></a>Para criar um projeto de pasta de trabalho do Excel

- Crie um projeto de pasta de trabalho do Excel com o nome **MyExcelRibbon**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho no designer e adiciona o projeto **MyExcelRibbon** ao **Gerenciador de soluções**.

## <a name="create-actions-panes"></a><a name="BKMK_CreateActionsPanes"></a> Criar painéis de ações
 Adicione dois painéis de ações personalizadas ao projeto. Posteriormente, você adicionará botões que mostram e ocultarão esses painéis de ações na guia personalizado.

### <a name="to-create-actions-panes"></a>Para criar painéis de ações

1. No menu **Projeto**, escolha **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **ActionsPaneControl** e, em seguida, escolha **Adicionar**.

     O arquivo **ActionsPaneControl1. cs** ou **ActionsPaneControl1. vb** é aberto no designer.

3. Na guia **controles comuns** da caixa de **ferramentas**, adicione um rótulo à superfície do designer.

4. Na janela **Propriedades** , defina a propriedade **Text** de Label1 para o **painel actions 1**.

5. Repita as etapas 1 a 5 para criar um segundo painel e rótulo de ações. Defina a propriedade **texto** do segundo rótulo para o **painel Ações 2**.

## <a name="create-a-custom-tab"></a><a name="BKMK_CreateCustomTab"></a> Criar uma guia personalizada
 Uma das diretrizes de design de aplicativos do Office é que os usuários sempre devem ter o controle da interface do usuário do aplicativo do Office. Para adicionar esse recurso aos painéis de ações, você pode adicionar botões que mostram e ocultam cada painel de ações de uma guia personalizada na faixa de faixas. Para criar uma guia personalizada, adicione um item **da faixa de Ribbon (designer visual)** ao projeto. O designer ajuda você a adicionar e posicionar controles, definir propriedades de controle e manipular eventos de controle.

### <a name="to-create-a-custom-tab"></a>Para criar uma guia personalizada

1. No menu **Projeto**, escolha **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)**.

3. Altere o nome da nova faixa de forma para **MyRibbon** e escolha **Adicionar**.

     O arquivo **MyRibbon. cs** ou **MyRibbon. vb** é aberto no designer de faixa de faixas e exibe uma guia e um grupo padrão.

4. No designer de faixa de faixas, escolha a guia padrão.

5. Na janela **Propriedades** , expanda a propriedade **ControlID** e defina a propriedade **ControlIdType** como **personalizada**.

6. Defina a propriedade **rótulo** como **minha guia personalizada**.

7. No designer de faixa de faixas, escolha **grupo1**.

8. Na janela **Propriedades** , defina **rótulo** como **Gerenciador do painel de ações**.

9. Na guia **controles da faixa** de **ferramentas** do Office, arraste um botão para o **grupo1**.

10. Selecione **Button1**.

11. Na janela **Propriedades** , defina **rótulo** para **mostrar o painel de ações 1**.

12. Adicione um segundo botão ao **grupo1** e defina a propriedade **rótulo** para **mostrar o painel de ações 2**.

13. Na guia **controles da faixa** de **ferramentas** do Office, arraste um controle **ToggleButton** para o **grupo1**.

14. Defina a propriedade **rótulo** para **ocultar o painel Ações**.

## <a name="hide-and-show-actions-panes-by-using-buttons-on-the-custom-tab"></a><a name="BKMK_HideShowActionsPane"></a> Ocultar e mostrar painéis de ações usando botões na guia personalizada
 A última etapa é adicionar o código que responde ao usuário. Adicione manipuladores de eventos para os <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> eventos dos dois botões e o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. Adicione código a esses manipuladores de eventos para habilitar a ocultação e a exibição dos painéis de ações.

### <a name="to-hide-and-show-actions-panes-by-using-buttons-in-the-custom-tab"></a>Para ocultar e mostrar painéis de ações usando botões na guia personalizado

1. No **Gerenciador de soluções**, abra o menu de atalho para *MyRibbon. cs* ou *MyRibbon. vb* e escolha **Exibir código**.

2. Adicione o código a seguir à parte superior da `MyRibbon` classe. Esse código cria dois objetos do painel Ações.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet1":::

3. Substitua o método `MyRibbon_Load` pelo seguinte código. Esse código adiciona os objetos do painel Ações à <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> coleção e oculta os objetos de exibição. O código do Visual C# também anexa delegados a vários eventos de controle da faixa de faixas.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet2":::

4. Adicione os três métodos do manipulador de eventos a seguir à `MyRibbon` classe. Esses métodos manipulam os <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> eventos dos dois botões e o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. Os manipuladores de eventos para button1 e Button2 mostram painéis de ações alternativas. O manipulador de eventos para toggleButton1 mostra e oculta o painel Ações ativas.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet3":::

## <a name="test-the-custom-tab"></a>Testar a guia personalizada
 Quando você executa o projeto, o Excel é iniciado e a guia **minha guia personalizada** é exibida na faixa de faixas. Escolha os botões na **minha guia personalizada** para mostrar e ocultar os painéis de ações.

### <a name="to-test-the-custom-tab"></a>Para testar a guia personalizada

1. Pressione **F5** para executar o projeto.

2. Escolha a guia **minha guia personalizada** .

3. No grupo **Gerenciador do painel Ações personalizadas** , escolha **Mostrar painel de ações 1**.

     O painel Ações será exibido e exibirá o rótulo de **ações painel 1**.

4. Escolha **Mostrar painel de ações 2**.

     O painel Ações é exibido e exibe o **painel Ações** de rótulo 2.

5. Escolha **ocultar painel Ações**.

     Os painéis de ações não são mais visíveis.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como personalizar a interface do usuário do Office a partir destes tópicos:

- Adicione a interface do usuário baseada em contexto a qualquer personalização no nível do documento. Para obter mais informações, consulte [visão geral do painel Ações](../vsto/actions-pane-overview.md).

- Estenda um formulário padrão ou personalizado do Microsoft Office Outlook. Para obter mais informações, consulte [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).

## <a name="see-also"></a>Consulte também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer da faixa de opções](../vsto/ribbon-designer.md)
- [Personalizar uma faixa de faixas para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [Como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [Como alterar a posição de uma guia na faixa de forma](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)
- [Como: adicionar controles ao modo de exibição de Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Visão geral do modelo de objeto Ribbon](../vsto/ribbon-object-model-overview.md)
