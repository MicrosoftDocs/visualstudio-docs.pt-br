---
title: 'Passo a passo: Exibir painéis de tarefas personalizados com mensagens de email no Outlook'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], displaying with e-mail messages
- displaying custom task panes in e-mail
- e-mail [Office development in Visual Studio], custom task panes displayed in
- custom task panes [Office development in Visual Studio], displaying with e-mail messages
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1c25121e96005486450397938aad3c24f89d26cc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49828462"
---
# <a name="walkthrough-display-custom-task-panes-with-email-messages-in-outlook"></a>Passo a passo: Exibir painéis de tarefas personalizados com mensagens de email no Outlook
  Este passo a passo demonstra como exibir uma instância exclusiva de cada mensagem de email que é criado ou aberto um painel de tarefas personalizado. Os usuários podem exibir ou ocultar o painel de tarefas personalizado usando um botão na faixa de opções de cada mensagem de email.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Para exibir um painel de tarefas personalizado com o windows Explorer ou o Inspetor vários, você deve criar uma instância do painel de tarefas personalizado para cada janela que é aberta. Para obter mais informações sobre o comportamento dos painéis de tarefas personalizados no Outlook windows, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
> [!NOTE]  
>  Este passo a passo apresenta o código de suplemento do VSTO em pequenas seções para tornar mais fácil discutir a lógica por trás do código.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Projetando a interface do usuário (IU) do painel de tarefas personalizado.  
  
-   Criando uma interface do usuário da faixa de opções personalizada.  
  
-   Exibindo a interface de usuário da faixa de opções personalizada com mensagens de email.  
  
-   Criando uma classe para gerenciar janelas de inspeção e painéis de tarefas personalizados.  
  
-   Inicializando e limpando recursos usados pelo suplemento do VSTO.  
  
-   Sincronizando o botão de alternância de faixa de opções com o painel de tarefas personalizado.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
- Microsoft [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] ou o Microsoft Outlook 2010.  
  
  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como fazer os painéis de tarefas de uso do i: no Outlook?](http://go.microsoft.com/fwlink/?LinkID=130309).  
  
## <a name="create-the-project"></a>Criar o projeto  
 Painéis de tarefas personalizados são implementados nos suplementos do VSTO. Comece criando um projeto de suplemento do VSTO para Outlook.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar uma **do suplemento do Outlook** projeto com o nome **OutlookMailItemTaskPane**. Use o **do suplemento do Outlook** modelo de projeto. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o *ThisAddIn.cs* ou *ThisAddIn. vb* arquivo de código e adiciona os **OutlookMailItemTaskPane** projeto ao **Gerenciador de soluções**.  
  
## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Projetar a interface do usuário do painel de tarefas personalizado  
 Não há nenhum designer visual para painéis de tarefas personalizados, mas você pode criar um controle de usuário com a interface do usuário que você deseja. O painel de tarefas personalizado neste suplemento do VSTO tem uma interface do usuário simple que contém um <xref:System.Windows.Forms.TextBox> controle. Posteriormente neste passo a passo, você irá adicionar o controle de usuário para o painel de tarefas personalizado.  
  
### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Ao projetar a interface do usuário do painel de tarefas personalizado  
  
1.  Na **Gerenciador de soluções**, clique no **OutlookMailItemTaskPane** projeto.  
  
2.  Sobre o **Project** menu, clique em **adicionar controle de usuário**.  
  
3.  No **Adicionar Novo Item** diálogo caixa, altere o nome do controle de usuário para **TaskPaneControl**e, em seguida, clique em **adicionar**.  
  
     O controle de usuário é aberto no designer.  
  
4.  Dos **controles comuns** guia da **caixa de ferramentas**, arraste uma **caixa de texto** controle para o controle de usuário.  
  
## <a name="design-the-user-interface-of-the-ribbon"></a>Projetar a interface do usuário da faixa de opções  
 Uma das metas para este suplemento do VSTO é dar aos usuários uma maneira de ocultar ou exibir o painel de tarefas personalizado na faixa de opções de cada mensagem de email. Para fornecer a interface do usuário, crie uma interface do usuário da faixa de opções personalizada que exibe um botão de alternância que os usuários podem clicar para exibir ou ocultar o painel de tarefas personalizado.  
  
### <a name="to-create-a-custom-ribbon-ui"></a>Para criar uma interface do usuário da faixa de opções personalizada  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **faixa de opções (Visual Designer)**.  
  
3.  Altere o nome da nova faixa de opções para **ManageTaskPaneRibbon**e clique em **Add**.  
  
     O *ManageTaskPaneRibbon.cs* ou *ManageTaskPaneRibbon.vb* arquivo é aberto no Designer de faixa de opções e exibe um guia padrão e um grupo.  
  
4.  No Designer de faixa de opções, clique em **group1**.  
  
5.  No **propriedades** janela, defina as **rótulo** propriedade a ser **Gerenciador de tarefas do painel**.  
  
6.  Do **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste um controle de ToggleButton no **Gerenciador de tarefas do painel** grupo.  
  
7.  Clique em **toggleButton1**.  
  
8.  No **propriedades** janela, defina as **rótulo** propriedade a ser **Mostrar painel de tarefas**.  
  
## <a name="display-the-custom-ribbon-user-interface-with-email-messages"></a>Exibir a interface do usuário da faixa de opções personalizada com mensagens de email  
 O painel de tarefas personalizado que você cria neste passo a passo foi projetado para aparecer somente com o windows de inspetor que contêm mensagens de email. Portanto, defina as propriedades para exibir sua interface do usuário da faixa de opções personalizada apenas com essas janelas.  
  
### <a name="to-display-the-custom-ribbon-ui-with-email-messages"></a>Para exibir a interface de usuário da faixa de opções personalizada com mensagens de email  
  
1.  No Designer de faixa de opções, clique o **ManageTaskPaneRibbon** faixa de opções.  
  
2.  No **propriedades** janela, clique na lista suspensa lista ao lado **RibbonType**e selecione **Microsoft.Outlook.Mail.Compose** e  **Microsoft.Outlook.Mail.Read**.  
  
## <a name="create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>Crie uma classe para gerenciar janelas de inspeção e painéis de tarefas personalizados  
 Há vários casos em que o suplemento do VSTO deve identificar qual painel de tarefas personalizado está associado com uma mensagem de email específico. Esses casos incluem o seguinte:  
  
- Quando o usuário fecha uma mensagem de email. Nesse caso, o suplemento do VSTO deve remover o painel de tarefas personalizado correspondente para garantir que recursos usados pelo suplemento do VSTO são limpos corretamente.  
  
- Quando o usuário fechar o painel de tarefas personalizado. Nesse caso, o suplemento do VSTO deve atualizar o estado do botão de alternância na faixa de opções da mensagem de email.  
  
- Quando o usuário clica no botão de alternância na faixa de opções. Nesse caso, o suplemento do VSTO deve ocultar ou exibir o painel de tarefas correspondente.  
  
  Para habilitar o suplemento do VSTO controlar qual painel de tarefas personalizado está associado com cada mensagem de email abertos, crie uma classe personalizada que encapsula os pares de <xref:Microsoft.Office.Interop.Outlook.Inspector> e <xref:Microsoft.Office.Tools.CustomTaskPane> objetos. Essa classe cria um novo objeto de painel de tarefas personalizado para cada mensagem de email e exclui o painel de tarefas personalizado quando a mensagem de email correspondente é fechada.  
  
### <a name="to-create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>Para criar uma classe para gerenciar janelas de inspeção e painéis de tarefas personalizados  
  
1.  Na **Gerenciador de soluções**, com o botão direito do *ThisAddIn.cs* ou *ThisAddIn. vb* arquivo e, em seguida, clique em **Exibir código**.  
  
2.  Adicione as seguintes instruções à parte superior do arquivo.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#2)]
     [!code-vb[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#2)]  
  
3.  Adicione o seguinte código para o *ThisAddIn.cs* ou *ThisAddIn. vb* de arquivos, fora o `ThisAddIn` classe (para o Visual c#, adicione esse código o `OutlookMailItemTaskPane` namespace). O `InspectorWrapper` classe gerencia um par de <xref:Microsoft.Office.Interop.Outlook.Inspector> e <xref:Microsoft.Office.Tools.CustomTaskPane> objetos. Você concluirá a definição dessa classe nas etapas a seguir.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#3)]
     [!code-vb[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#3)]  
  
4.  Adicione o seguinte construtor após o código que você adicionou na etapa anterior. Este construtor cria e inicializa um novo painel de tarefas personalizado que está associado com o <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que é passado. No c#, o construtor também anexa os manipuladores de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> eventos do <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto e, o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> eventos do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#4)]
     [!code-vb[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#4)]  
  
5.  Adicione o seguinte método após o código que você adicionou na etapa anterior. Esse método é um manipulador de eventos para o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> eventos do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto está contido no `InspectorWrapper` classe. Esse código atualiza o estado do botão de alternância, sempre que o usuário abre ou fecha o painel de tarefas personalizado.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#5)]
     [!code-vb[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#5)]  
  
6.  Adicione o seguinte método após o código que você adicionou na etapa anterior. Esse método é um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> eventos do <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que contém a mensagem de email atual. O manipulador de eventos libera recursos quando a mensagem de email é fechada. O manipulador de eventos também remove o painel de tarefas personalizado atual do `CustomTaskPanes` coleção. Isso ajuda a impedir que várias instâncias do painel de tarefas personalizado quando a próxima mensagem de email é aberta.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#6)]
     [!code-vb[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#6)]  
  
7.  Adicione o seguinte código após o código que você adicionou na etapa anterior. Posteriormente neste passo a passo, você chamará essa propriedade de um método na interface do usuário da faixa de opções personalizada para exibir ou ocultar o painel de tarefas personalizado.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#7)]
     [!code-vb[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#7)]  
  
## <a name="initialize-and-clean-up-resources-used-by-the-add-in"></a>Inicializar e limpar os recursos usados pelo suplemento  
 Adicione código para o `ThisAddIn` classe para inicializar o suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo suplemento do VSTO quando ela for descarregada. Inicializar o suplemento do VSTO, configurando um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> eventos e passando todas as mensagens de email existente para esse manipulador de eventos. Quando o suplemento do VSTO é descarregado, desanexar o manipulador de eventos e limpar objetos usados pelo suplemento do VSTO.  
  
### <a name="to-initialize-and-clean-up-resources-used-by-the-vsto-add-in"></a>Para inicializar e limpar os recursos usados pelo suplemento do VSTO  
  
1. No *ThisAddIn.cs* ou *ThisAddIn. vb* arquivo, localize a definição do `ThisAddIn` classe.  
  
2. Adicione as seguintes declarações para o `ThisAddIn` classe:  
  
   - O `inspectorWrappersValue` campo contém todos os <xref:Microsoft.Office.Interop.Outlook.Inspector> e `InspectorWrapper` objetos que são gerenciados pelo suplemento do VSTO.  
  
   - O `inspectors` campo mantém uma referência para a coleção de janelas de inspeção na instância atual do Outlook. Esta referência impede que o coletor de lixo de liberar a memória que contém o manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento, que você irá declarar na próxima etapa.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#8)]
     [!code-vb[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#8)]  
  
3. Substitua o `ThisAddIn_Startup` método com o código a seguir. Esse código anexa um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento e ele passa cada existente <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto para o manipulador de eventos. Se o usuário carrega o suplemento do VSTO depois que o Outlook já está em execução, o suplemento do VSTO usa essas informações para criar painéis de tarefas personalizados para todas as mensagens de email que já estão abertas.  
  
    [!code-csharp[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#9)]
    [!code-vb[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#9)]  
  
4. Substitua o `ThisAddIn_ShutDown` método com o código a seguir. Esse código desanexa o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> manipulador de eventos e limpa os objetos usados pelo suplemento do VSTO.  
  
    [!code-csharp[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#10)]
    [!code-vb[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#10)]  
  
5. Adicione o seguinte <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> manipulador de eventos para o `ThisAddIn` classe. Se um novo <xref:Microsoft.Office.Interop.Outlook.Inspector> contém uma mensagem de email, o método cria uma instância de um novo `InspectorWrapper` objeto para gerenciar a relação entre a mensagem de email e o painel de tarefas correspondente.  
  
    [!code-csharp[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#11)]
    [!code-vb[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#11)]  
  
6. Adicione a seguinte propriedade para o `ThisAddIn` classe. Essa propriedade expõe particular `inspectorWrappersValue` campo para o código fora de `ThisAddIn` classe.  
  
    [!code-csharp[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#12)]
    [!code-vb[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#12)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Compile o projeto para garantir que ele foi compilado sem erros.  
  
### <a name="to-build-your-project"></a>Para compilar seu projeto  
  
1.  Na **Gerenciador de soluções**, com o botão direito do **OutlookMailItemTaskPane** do projeto e, em seguida, clique em **Build**. Verifique se que o projeto é compilado sem erros.  
  
## <a name="synchronize-the-ribbon-toggle-button-with-the-custom-task-pane"></a>Sincronizar o botão de alternância de faixa de opções com o painel de tarefas personalizado  
 O botão de alternância parecerão ser pressionado quando o painel de tarefas está visível e parece não ser pressionado quando o painel de tarefas está oculta. Para sincronizar o estado do botão com o painel de tarefas personalizado, modifique o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> manipulador de eventos do botão de alternância.  
  
### <a name="to-synchronize-the-custom-task-pane-with-the-toggle-button"></a>Para sincronizar o painel de tarefas personalizado com o botão de alternância  
  
1.  No Designer de faixa de opções, clique duas vezes o **Mostrar painel de tarefas** botão de alternância.  
  
     Visual Studio gera automaticamente um manipulador de eventos chamado `toggleButton1_Click`, que trata o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. O Visual Studio também abre a *ManageTaskPaneRibbon.cs* ou *ManageTaskPaneRibbon.vb* arquivo no Editor de códigos.  
  
2.  Adicione as seguintes instruções na parte superior do *ManageTaskPaneRibbon.cs* ou *ManageTaskPaneRibbon.vb* arquivo.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#14)]
     [!code-vb[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#14)]  
  
3.  Substitua o `toggleButton1_Click` manipulador de eventos com o código a seguir. Quando o usuário clica no botão de alternância, esse método oculta ou exibe o painel de tarefas personalizado que está associado com a janela Inspetor atual.  
  
     [!code-csharp[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#15)]
     [!code-vb[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#15)]  
  
## <a name="test-the-project"></a>O projeto de teste  
 Quando você inicia a depuração do projeto, abre o Outlook e o suplemento do VSTO é carregado. O suplemento do VSTO exibe uma instância exclusiva do painel de tarefas personalizado com cada mensagem de email que é aberta. Crie várias novas mensagens de email para testar o código.  
  
### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1. Pressione **F5**.  
  
2. No Outlook, clique em **New** para criar uma nova mensagem de email.  
  
3. Na faixa de opções da mensagem de email, clique no **Add-Ins** guia e, em seguida, clique no **Mostrar painel de tarefas** botão.  
  
    Verificar se um painel de tarefas com o título **meu painel de tarefas** é exibida com a mensagem de email.  
  
4. No painel de tarefas, digite **primeiro painel de tarefas** na caixa de texto.  
  
5. Feche o painel de tarefas.  
  
    Verifique o estado do **Mostrar painel de tarefas** botão muda para que ele não seja pressionado.  
  
6. Clique o **Mostrar painel de tarefas** novamente no botão.  
  
    Verifique se o painel de tarefas é aberta e que a caixa de texto ainda contém a cadeia de caracteres **primeiro painel de tarefas**.  
  
7. No Outlook, clique em **New** para criar uma segunda mensagem de email.  
  
8. Na faixa de opções da mensagem de email, clique no **Add-Ins** guia e, em seguida, clique no **Mostrar painel de tarefas** botão.  
  
    Verificar se um painel de tarefas com o título **meu painel de tarefas** é exibida com a mensagem de email, e a caixa de texto nesse painel de tarefas está vazia.  
  
9. No painel de tarefas, digite **segundo painel de tarefas** na caixa de texto.  
  
10. Altere o foco para a primeira mensagem de email.  
  
     Verifique se o painel de tarefas que está associado essa mensagem de email ainda exibe **primeiro painel de tarefas** na caixa de texto.  
  
    Este suplemento do VSTO também lida com mais cenários avançados que você pode experimentar. Por exemplo, você pode testar o comportamento ao exibir emails usando o **Próximo Item** e **Item anterior** botões. Você também pode testar o comportamento ao descarregar o suplemento do VSTO, abrir várias mensagens de email e, em seguida, recarregue o suplemento do VSTO.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como criar painéis de tarefas personalizados com estes tópicos:  
  
-   Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
-   Automatize um aplicativo do Microsoft Office usando o painel de tarefas personalizado. Para obter mais informações, consulte [instruções passo a passo: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md).  
  
-   Crie um botão de faixa de opções no Excel que pode ser usado para ocultar ou exibir um painel de tarefas personalizado. Para obter mais informações, consulte [instruções passo a passo: sincronizar um painel de tarefas personalizado com um botão da faixa de opções](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md).  
  
## <a name="see-also"></a>Consulte também  
 [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)   
 [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)   
 [Passo a passo: Automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)   
 [Passo a passo: Sincronizar um painel de tarefas personalizado com um botão da faixa de opções](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)   
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)  
  
  