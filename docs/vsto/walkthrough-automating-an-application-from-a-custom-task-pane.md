---
title: 'Passo a passo: Automatizar um aplicativo de um painel de tarefas personalizado'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio], custom task panes
- automating Office applications
- custom task panes [Office development in Visual Studio], automating applications
- custom task panes [Office development in Visual Studio], PowerPoint
- task panes [Office development in Visual Studio], automating applications
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 25d6dd29f989f1ea2bbf95ce2b32e7d031e1953e
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669827"
---
# <a name="walkthrough-automate-an-application-from-a-custom-task-pane"></a>Passo a passo: Automatizar um aplicativo de um painel de tarefas personalizado
  Este passo a passo demonstra como criar um painel de tarefas personalizado que automatiza o PowerPoint. O painel de tarefas personalizado insere as datas em um slide quando o usuário clica em um <xref:System.Windows.Forms.MonthCalendar> controle que esteja no painel de tarefas personalizado.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Embora este passo a passo usa o PowerPoint especificamente, os conceitos demonstrados pelo passo a passo são aplicáveis a todos os aplicativos que estão listados acima.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Projetando a interface do usuário do painel de tarefas personalizado.  
  
-   Automatizar o PowerPoint no painel de tarefas personalizado.  
  
-   Exibindo o painel de tarefas personalizado no PowerPoint.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft PowerPoint 2010 ou [!INCLUDE[PowerPoint_15_short](../vsto/includes/powerpoint-15-short-md.md)].  
  
## <a name="create-the-add-in-project"></a>Criar o projeto de suplemento  
 A primeira etapa é criar um projeto de suplemento do VSTO para PowerPoint.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de suplemento do VSTO do PowerPoint com o nome **MyAddIn**, usando o modelo de projeto do suplemento do PowerPoint. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **ThisAddIn.cs** ou **ThisAddIn. vb** arquivo de código e adiciona os **MyAddIn** projeto ao **Gerenciador de soluções**.  
  
## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Projetar a interface do usuário do painel de tarefas personalizado  
 Não há nenhum designer visual para painéis de tarefas personalizados, mas você pode criar um controle de usuário com o layout desejado. Posteriormente neste passo a passo, você irá adicionar o controle de usuário para o painel de tarefas personalizado.  
  
#### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Ao projetar a interface do usuário do painel de tarefas personalizado  
  
1.  Sobre o **Project** menu, clique em **adicionar controle de usuário**.  
  
2.  No **Adicionar Novo Item** diálogo caixa, altere o nome do controle de usuário para **MyUserControl**e clique em **adicionar**.  
  
     O controle de usuário é aberto no designer.  
  
3.  Dos **controles comuns** guia da **caixa de ferramentas**, arraste uma **MonthCalendar** controle para o controle de usuário.  
  
     Se o **MonthCalendar** controle é maior do que a superfície de design do controle de usuário, redimensione o controle de usuário de acordo com as **MonthCalendar** controle.  
  
## <a name="automate-powerpoint-from-the-custom-task-pane"></a>Automatizar o PowerPoint no painel de tarefas personalizado  
 A finalidade do suplemento do VSTO é colocar uma data selecionada no primeiro slide da apresentação ativa. Use o <xref:System.Windows.Forms.MonthCalendar.DateChanged> evento do controle para adicionar a data selecionada sempre que ele é alterado.  
  
### <a name="to-automate-powerpoint-from-the-custom-task-pane"></a>Para automatizar o PowerPoint no painel de tarefas personalizado  
  
1.  No designer, clique duas vezes o <xref:System.Windows.Forms.MonthCalendar> controle.  
  
     O **MyUserControl.cs** ou **MyUserControl.vb** arquivo é aberto e um manipulador de eventos para o <xref:System.Windows.Forms.MonthCalendar.DateChanged> evento for criado.  
  
2.  Adicione o seguinte código à parte superior do arquivo. Esse código cria aliases para o <xref:Microsoft.Office.Core> e <xref:Microsoft.Office.Interop.PowerPoint> namespaces.  
  
     [!code-csharp[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#1)]
     [!code-vb[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#1)]  
  
3.  Adicione o seguinte código para o `MyUserControl` classe. Esse código declara uma <xref:Microsoft.Office.Interop.PowerPoint.Shape> objeto como um membro de `MyUserControl`. Na etapa a seguir, você usará isso <xref:Microsoft.Office.Interop.PowerPoint.Shape> para adicionar uma caixa de texto a um slide na apresentação ativa.  
  
     [!code-csharp[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#2)]
     [!code-vb[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#2)]  
  
4.  Substitua o `monthCalendar1_DateChanged` manipulador de eventos com o código a seguir. Esse código adiciona uma caixa de texto ao primeiro slide na apresentação ativa e, em seguida, adiciona a data atualmente selecionada à caixa de texto. Esse código usa o `Globals.ThisAddIn` objeto para acessar o modelo de objeto do PowerPoint.  
  
     [!code-csharp[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#3)]
     [!code-vb[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#3)]  
  
5.  Na **Gerenciador de soluções**, com o botão direito do **MyAddIn** do projeto e, em seguida, clique em **Build**. Verifique se o projeto é compilado sem erros.  
  
## <a name="display-the-custom-task-pane"></a>Exibir o painel de tarefas personalizado  
 Para exibir o painel de tarefas personalizado quando o suplemento do VSTO é iniciado, adicione o controle de usuário ao painel de tarefas no <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos do que o suplemento do VSTO.  
  
### <a name="to-display-the-custom-task-pane"></a>Para exibir o painel de tarefas personalizado  
  
1.  Na **Gerenciador de soluções**, expanda **PowerPoint**.  
  
2.  Clique com botão direito **ThisAddIn.cs** ou **ThisAddIn. vb** e clique em **Exibir código**.  
  
3.  Adicione o seguinte código para o `ThisAddIn` classe. Esse código declara as instâncias de `MyUserControl` e <xref:Microsoft.Office.Tools.CustomTaskPane> como membros do `ThisAddIn` classe.  
  
     [!code-vb[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#4)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#4)]  
  
4.  Substitua o `ThisAddIn_Startup` manipulador de eventos com o código a seguir. Esse código cria uma nova <xref:Microsoft.Office.Tools.CustomTaskPane> adicionando o `MyUserControl` do objeto para o `CustomTaskPanes` coleção. O código também exibe o painel de tarefas.  
  
     [!code-vb[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#5)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#5)]  
  
## <a name="test-the-add-in"></a>Testar o suplemento  
 Quando você executa o projeto, o PowerPoint é aberto e o suplemento do VSTO exibe o painel de tarefas personalizado. Clique o <xref:System.Windows.Forms.MonthCalendar> controle para testar o código.  
  
### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Confirme se o painel de tarefas personalizado está visível.  
  
3.  Clique em uma data a <xref:System.Windows.Forms.MonthCalendar> controle no painel de tarefas.  
  
     A data é inserida no primeiro slide na apresentação ativa.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como criar painéis de tarefas personalizados com estes tópicos:  
  
-   Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
-   Crie um botão da faixa de opções que pode ser usado para ocultar ou exibir um painel de tarefas personalizado. Para obter mais informações, consulte [instruções passo a passo: sincronizar um painel de tarefas personalizado com um botão da faixa de opções](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md).  
  
-   Crie um painel de tarefas personalizado para cada mensagem de email que é aberto no Outlook. Para obter mais informações, consulte [instruções passo a passo: exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md).  
  
## <a name="see-also"></a>Consulte também  
 [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)   
 [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)   
 [Passo a passo: Sincronizar um painel de tarefas personalizado com um botão da faixa de opções](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)   
 [Passo a passo: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)  
  
  