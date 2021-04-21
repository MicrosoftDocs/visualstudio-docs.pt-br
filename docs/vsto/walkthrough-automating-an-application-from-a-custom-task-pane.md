---
title: 'Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado'
description: Crie um painel de tarefas personalizado que automatiza o Microsoft PowerPoint inserindo datas em um slide quando o usuário clica em um controle MonthCalendar no painel de tarefas personalizado.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f57ad0c858abb5f151e1b425224b5af34d464c0f
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824660"
---
# <a name="walkthrough-automate-an-application-from-a-custom-task-pane"></a>Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado
  Este tutorial demonstra como criar um painel de tarefas personalizado que automatiza o PowerPoint. O painel de tarefas personalizado insere datas em um slide quando o usuário clica <xref:System.Windows.Forms.MonthCalendar> em um controle que está no painel de tarefas personalizado.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 Embora este passo a passos use o PowerPoint especificamente, os conceitos demonstrados por instruções são aplicáveis a todos os aplicativos listados acima.

 Este passo a passo ilustra as seguintes tarefas:

- Criando a interface do usuário do painel de tarefas personalizado.

- Automatizando o PowerPoint do painel de tarefas personalizado.

- Exibindo o painel de tarefas personalizado no PowerPoint.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft PowerPoint 2010 ou [!INCLUDE[PowerPoint_15_short](../vsto/includes/powerpoint-15-short-md.md)] .

## <a name="create-the-add-in-project"></a>Criar o projeto de suplemento
 A primeira etapa é criar um projeto de suplemento do VSTO para o PowerPoint.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de suplemento do VSTO do PowerPoint com o nome **MyAddin**, usando o modelo de projeto de suplemento do PowerPoint. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo de código **ThisAddIn. cs** ou **ThisAddIn. vb** e adiciona o projeto **MyAddin** a **Gerenciador de soluções**.

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Criar a interface do usuário do painel de tarefas personalizado
 Não há nenhum designer visual para painéis de tarefas personalizados, mas você pode criar um controle de usuário com o layout desejado. Mais adiante neste tutorial, você adicionará o controle de usuário ao painel de tarefas personalizado.

#### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Para criar a interface do usuário do painel de tarefas personalizado

1. No menu **projeto** , clique em **Adicionar controle de usuário**.

2. Na caixa de diálogo **Adicionar novo item** , altere o nome do controle de usuário para **MyUserControl** e clique em **Adicionar**.

     O controle de usuário é aberto no designer.

3. Na guia **controles comuns** da caixa de **ferramentas**, arraste um controle **MonthCalendar** para o controle de usuário.

     Se o controle **MonthCalendar** for maior que a superfície de design do controle de usuário, redimensione o controle de usuário para ajustá-lo ao controle **MonthCalendar** .

## <a name="automate-powerpoint-from-the-custom-task-pane"></a>Automatizar o PowerPoint no painel de tarefas personalizado
 A finalidade do suplemento do VSTO é colocar uma data selecionada no primeiro slide da apresentação ativa. Use o <xref:System.Windows.Forms.MonthCalendar.DateChanged> evento do controle para adicionar a data selecionada sempre que ela for alterada.

### <a name="to-automate-powerpoint-from-the-custom-task-pane"></a>Para automatizar o PowerPoint a partir do painel de tarefas personalizado

1. No designer, clique duas vezes no <xref:System.Windows.Forms.MonthCalendar> controle.

     O arquivo **MyUserControl. cs** ou **MyUserControl. vb** é aberto e um manipulador de eventos para o <xref:System.Windows.Forms.MonthCalendar.DateChanged> evento é criado.

2. Adicione o código a seguir no início do arquivo. Esse código cria aliases para os <xref:Microsoft.Office.Core> namespaces do e do [PowerPoint](/previous-versions/office/developer/office-2010/ff763170%28v%3doffice.14%29) .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb" id="Snippet1":::

3. Adicione o código a seguir à classe `MyUserControl` . Esse código declara um objeto [Shape](/previous-versions/office/developer/office-2010/ff760244(v=office.14)) como um membro de `MyUserControl` . Na etapa a seguir, você usará essa [forma](/previous-versions/office/developer/office-2010/ff760244(v=office.14)) para adicionar uma caixa de texto a um slide na apresentação ativa.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb" id="Snippet2":::

4. Substitua o `monthCalendar1_DateChanged` manipulador de eventos pelo código a seguir. Esse código adiciona uma caixa de texto ao primeiro slide da apresentação ativa e, em seguida, adiciona a data atualmente selecionada à caixa de texto. Esse código usa o `Globals.ThisAddIn` objeto para acessar o modelo de objeto do PowerPoint.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb" id="Snippet3":::

5. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **MyAddin** e clique em **Compilar**. Verifique se o projeto é compilado sem erros.

## <a name="display-the-custom-task-pane"></a>Exibir o painel de tarefas personalizado
 Para exibir o painel de tarefas personalizado quando o suplemento do VSTO for iniciado, adicione o controle de usuário ao painel de tarefas no <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos do suplemento do VSTO.

### <a name="to-display-the-custom-task-pane"></a>Para exibir o painel de tarefas personalizado

1. Em **Gerenciador de soluções**, expanda **PowerPoint**.

2. Clique com o botão direito do mouse em **ThisAddIn. cs** ou em **ThisAddIn. vb** e clique em **Exibir código**.

3. Adicione o código a seguir à classe `ThisAddIn` . Esse código declara instâncias do `MyUserControl` e <xref:Microsoft.Office.Tools.CustomTaskPane> como membros da `ThisAddIn` classe.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs" id="Snippet4":::

4. Substitua o `ThisAddIn_Startup` manipulador de eventos pelo código a seguir. Esse código cria um novo <xref:Microsoft.Office.Tools.CustomTaskPane> adicionando o `MyUserControl` objeto à `CustomTaskPanes` coleção. O código também exibe o painel de tarefas.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs" id="Snippet5":::

## <a name="test-the-add-in"></a>Testar o suplemento
 Quando você executa o projeto, o PowerPoint é aberto e o suplemento do VSTO exibe o painel de tarefas personalizado. Clique no <xref:System.Windows.Forms.MonthCalendar> controle para testar o código.

### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5** para executar o projeto.

2. Confirme se o painel de tarefas personalizado está visível.

3. Clique em uma data no <xref:System.Windows.Forms.MonthCalendar> controle no painel de tarefas.

     A data é inserida no primeiro slide da apresentação ativa.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar painéis de tarefas personalizados a partir destes tópicos:

- Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

- Crie um botão da faixa de medida que possa ser usado para ocultar ou exibir um painel de tarefas personalizado. Para obter mais informações, consulte [Walkthrough: sincronizar um painel de tarefas personalizado com um botão Ribbon](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md).

- Crie um painel de tarefas personalizado para cada mensagem de email aberta no Outlook. Para obter mais informações, consulte [Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md).

## <a name="see-also"></a>Consulte também
- [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)
- [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [Walkthrough: sincronizar um painel de tarefas personalizado com um botão da faixa de das](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
