---
title: 'Passo a passo: Criando um fluxo de trabalho com associação e formulários de iniciação | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b6aafde6fed0a1f1722c2d355499523114aaaa00
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873871"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>Passo a passo: Criar um fluxo de trabalho com formulários de associação e iniciação
  Este passo a passo demonstra como criar um fluxo de trabalho sequencial básico que incorpora o uso de formulários de associação e iniciação. Esses são os formulários ASPX que permitem que os parâmetros a ser adicionado a um fluxo de trabalho quando ele pela primeira vez é associado pelo administrador do SharePoint (o formulário de associação), e quando o fluxo de trabalho é iniciado pelo usuário (o formulário de inicialização).  
  
 Este passo a passo descreve um cenário em que um usuário deseja criar um fluxo de trabalho de aprovação para relatórios de despesas que tem os seguintes requisitos:  
  
- Quando o fluxo de trabalho está associado uma lista, o administrador é solicitado com um formulário de associação no qual eles digitar um limite de dólar para relatórios de despesas.  
  
- Os funcionários carregar seus relatórios de despesas para a lista de documentos compartilhados, iniciar o fluxo de trabalho e, em seguida, insira o custo total do formulário de iniciação do fluxo de trabalho.  
  
- Se um relatório de despesas de funcionários total exceder o limite de predefinido do administrador, uma tarefa é criada para o gerente do funcionário aprovar o relatório de despesas. No entanto, se o total de relatórios de despesas de um funcionário é menor que ou igual ao limite de gastos, uma mensagem de aprovação automática é gravada para a lista de histórico do fluxo de trabalho.  
  
  Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um projeto de fluxo de trabalho sequencial de definição de lista do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
- Criando uma agenda de fluxo de trabalho.  
  
- Manipulação de eventos de atividade de fluxo de trabalho.  
  
- Criando formulários de associação e iniciação de fluxo de trabalho.  
  
- Associando o fluxo de trabalho.  
  
- O fluxo de trabalho é iniciado manualmente.  
  
> [!NOTE]  
>  Embora este passo a passo usa um projeto de fluxo de trabalho sequencial, o processo é o mesmo para fluxos de trabalho de máquina de estado.  
>   
>  Além disso, seu computador pode mostrar diferentes nomes ou localizações para alguns do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] elementos de interface do usuário nas instruções a seguir. O [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] edição que você tem e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e do SharePoint.  
  
-   Visual Studio.  
  
## <a name="create-a-sharepoint-sequential-workflow-project"></a>Criar um projeto de fluxo de trabalho sequencial do SharePoint
 Primeiro, crie um projeto de fluxo de trabalho sequencial no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Um fluxo de trabalho sequencial é uma série de etapas que executa em ordem até que a última atividade seja concluída. Neste procedimento, você criará um fluxo de trabalho sequencial que se aplica à lista de documentos compartilhados no SharePoint. Assistente do fluxo de trabalho permite associar o fluxo de trabalho com o site ou a definição de lista e permite determinar quando o fluxo de trabalho será iniciado.  
  
#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>Para criar um projeto de fluxo de trabalho sequencial do SharePoint  
  
1.  Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.  
  
2.  Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3.  No **modelos** painel, escolha o **o projeto do SharePoint 2010** modelo de projeto.  
  
4.  No **nome** , digite **ExpenseReport** e, em seguida, escolha o **Okey** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
5.  No **especificar o nível de site e segurança para depuração** , escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão para aceitar o site padrão e o nível de confiança.  
  
     Esta etapa também define o nível de confiança para a solução como solução de farm, que é a única opção disponível para projetos de fluxo de trabalho.  
  
6.  Na **Gerenciador de soluções**, escolha o nó do projeto.  
  
7.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
8.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
9. No **modelos** painel, escolha **fluxo de trabalho sequencial (somente solução de Farm)** modelo e, em seguida, escolha o **Add** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
10. No **especifique o nome do fluxo de trabalho para depuração** página, aceite o nome padrão (**ExpenseReport - Workflow1**). Mantenha o valor de tipo de modelo de fluxo de trabalho padrão (**fluxo de trabalho de lista)**. Escolha o botão **Avançar**.  
  
11. No **deseja que o Visual Studio associe automaticamente o fluxo de trabalho em uma sessão de depuração?** página, desmarque a caixa que associa automaticamente seu modelo de fluxo de trabalho se ela estiver marcada.  
  
     Esta etapa permite associar manualmente o fluxo de trabalho com a lista de documentos compartilhados no futuro, que exibe o formulário de associação.  
  
12. Escolha o **concluir** botão.  
  
## <a name="add-an-association-form-to-the-workflow"></a>Adicionar um formulário de associação para o fluxo de trabalho
 Em seguida, crie um. Formulário de associação de ASPX que aparece quando o administrador do SharePoint associa primeiro o fluxo de trabalho com um documento de relatório de despesas.  
  
#### <a name="to-add-an-association-form-to-the-workflow"></a>Para adicionar um formulário de associação para o fluxo de trabalho  
  
1.  Escolha o **Workflow1** nó no **Gerenciador de soluções**.  
  
2.  Na barra de menus, escolha **Project** > **Adicionar Novo Item** para exibir o **Add New Item** caixa de diálogo.  
  
3.  Na exibição de árvore de caixa de diálogo, expanda **Visual c#** ou **Visual Basic** (dependendo do idioma do projeto), expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  Na lista de modelos, escolha o **formulário de associação de fluxo de trabalho** modelo.  
  
5.  No **nome** texto, digite **ExpenseReportAssocForm.aspx**.  
  
6.  Escolha o **adicionar** botão para adicionar o formulário ao projeto.  
  
## <a name="designing-and-coding-the-association-form"></a>Criar e codificar o formulário de associação
 Neste procedimento, você pode introduzir funcionalidade para o formulário de associação, adicionando controles e código para ele.  
  
#### <a name="to-design-and-code-the-association-form"></a>Para criar e codificar o formulário de associação  
  
1.  No formulário de associação (ExpenseReportAssocForm.aspx), localize o `asp:Content` elemento que tem `ID="Main"`.  
  
2.  Diretamente após a primeira linha nesse elemento de conteúdo, adicione o seguinte código para criar um rótulo e uma caixa de texto que solicita o limite de aprovação de despesas (*AutoApproveLimit*):  
  
    ```aspx-csharp  
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />  
  
    <asp:TextBox ID="AutoApproveLimit" runat="server" />  
    <br /><br />  
    ```  
  
3.  Expanda o **ExpenseReportAssocForm.aspx** arquivo no **Gerenciador de soluções** para exibir seus arquivos dependentes.  
  
    > [!NOTE]  
    >  Se seu projeto estiver no [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)], você deve escolher o **exibir todos os arquivos** botão para executar esta etapa.  
  
4.  Abra o menu de atalho para o arquivo ExpenseReportAssocForm.aspx e escolha **Exibir código**.  
  
5.  Substitua o `GetAssociationData` método com:  
  
    ```vb  
    Private Function GetAssociationData() As String  
        ' TODO: Return a string that contains the association data that   
        ' will be passed to the workflow. Typically, this is in XML   
        ' format.  
        Return Me.AutoApproveLimit.Text  
    End Function  
    ```  
  
    ```csharp  
    private string GetAssociationData()  
    {  
        // TODO: Return a string that contains the association data that   
        // will be passed to the workflow. Typically, this is in XML   
        // format.  
        return this.AutoApproveLimit.Text;  
    }  
    ```  
  
## <a name="add-an-initiation-form-to-the-workflow"></a>Adicionar um formulário de inicialização para o fluxo de trabalho
 Em seguida, crie o formulário de iniciação que aparece quando os usuários executam o fluxo de trabalho em relação a seus relatórios de despesas.  
  
#### <a name="to-create-an-initiation-form"></a>Para criar um formulário de inicialização  
  
1.  Escolha o **Workflow1** nó no **Gerenciador de soluções**.  
  
2.  Na barra de menus, escolha **Project** > **Adicionar Novo Item** exibir a **Add New Item** caixa de diálogo.  
  
3.  Na exibição de árvore de caixa de diálogo, expanda **Visual c#** ou **Visual Basic** (dependendo do idioma do projeto), expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  Na lista de modelos, escolha o **formulário de iniciação do fluxo de trabalho** modelo.  
  
5.  No **nome** texto, digite **ExpenseReportInitForm.aspx**.  
  
6.  Escolha o **adicionar** botão para adicionar o formulário ao projeto.  
  
## <a name="designing-and-coding-the-initiation-form"></a>Criar e codificar o formulário de iniciação
 Em seguida, coloque a funcionalidade para o formulário de iniciação adicionando controles e código para ele.  
  
#### <a name="to-code-the-initiation-form"></a>Para o formulário de iniciação de código  
  
1.  No formulário de iniciação (ExpenseReportInitForm.aspx), localize o `asp:Content` elemento que contém `ID="Main"`.  
  
2.  Diretamente após a primeira linha nesse elemento de conteúdo, adicione o seguinte código para criar um rótulo e uma caixa de texto que exibe o limite de aprovação de despesas (*AutoApproveLimit*) que foi inserido no formulário de associação e outro rótulo e caixa de texto para solicitar o total de despesas (*ExpenseTotal*):  
  
    ```aspx-csharp  
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />  
  
    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />  
    <br /><br />  
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />  
  
    <asp:TextBox ID="ExpenseTotal" runat="server" />  
    <br /><br />  
    ```  
  
3.  Expanda o **ExpenseReportInitForm.aspx** arquivo no **Gerenciador de soluções** para exibir seus arquivos dependentes.  
  
4.  Abra o menu de atalho para o arquivo ExpenseReportInitForm.aspx e escolha **Exibir código**.  
  
5.  Substitua o `Page_Load` método com o exemplo a seguir:  
  
    ```vb  
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As   
      EventArgs) Handles Me.Load  
        InitializeParams()  
        Me.AutoApproveLimit.Text = workflowList.WorkflowAssociations(New   
          Guid(associationGuid)).AssociationData  
        ' Optionally, add code here to pre-populate your form fields.  
    End Sub  
    ```  
  
    ```csharp  
    protected void Page_Load(object sender, EventArgs e)  
    {  
        InitializeParams();  
        this.AutoApproveLimit.Text =   
          workflowList.WorkflowAssociations[new   
          Guid(associationGuid)].AssociationData;  
    }  
    ```  
  
6.  Substitua o `GetInitiationData` método com o exemplo a seguir:  
  
    ```vb  
    ' This method is called when the user clicks the button to start the workflow.  
    Private Function GetInitiationData() As String  
        Return Me.ExpenseTotal.Text  
        ' TODO: Return a string that contains the initiation data that   
        ' will be passed to the workflow. Typically, this is in XML   
        ' format.  
        Return String.Empty  
    End Function  
    ```  
  
    ```csharp  
    // This method is called when the user clicks the button to start the workflow.          
    private string GetInitiationData()  
    {  
        // TODO: Return a string that contains the initiation data that   
        // will be passed to the workflow. Typically, this is in XML   
        // format.  
        return this.ExpenseTotal.Text;  
    }  
    ```  
  
## <a name="cutomize-the-workflow"></a>Personalizar o fluxo de trabalho
 Em seguida, personalize o fluxo de trabalho. Posteriormente, você associará dois formulários para o fluxo de trabalho.  
  
#### <a name="to-customize-the-workflow"></a>Para personalizar o fluxo de trabalho  
  
1.  Exiba o fluxo de trabalho no designer de fluxo de trabalho abrindo Workflow1 no projeto.  
  
2.  No **caixa de ferramentas**, expanda o **Windows Workflow v3.0** nó e localize o **IfElse** atividade.  
  
3.  Adicione esta atividade ao fluxo de trabalho executando uma das seguintes etapas:  
  
    -   Abra o menu de atalho para o **IfElse** atividade, escolha **cópia**, abra o menu de atalho para a linha sob o **onWorkflowActivated1** atividade no designer de fluxo de trabalho, e, em seguida, escolha **colar**.  
  
    -   Arraste o **IfElse** atividade da **caixa de ferramentas**e conectá-lo para a linha no **onWorkflowActiviated1** atividade no designer de fluxo de trabalho.  
  
4.  Na caixa de ferramentas, expanda o **fluxo de trabalho do SharePoint** nó e localize o **CreateTask** atividade.  
  
5.  Adicione esta atividade ao fluxo de trabalho executando uma das seguintes etapas:  
  
    -   Abra o menu de atalho para o **CreateTask** atividade, escolha **cópia**, abra o menu de atalho para um dos dois **soltar atividades aqui** áreas dentro do  **IfElseActivity1** no designer de fluxo de trabalho e, em seguida, escolha **colar**.  
  
    -   Arraste o **CreateTask** atividade da **caixa de ferramentas** em um dos dois **soltar atividades aqui** áreas dentro do **IfElseActivity1**.  
  
6.  No **propriedades** janela, insira um valor da propriedade *taskToken* para o **CorrelationToken** propriedade.  
  
7.  Expanda o **CorrelationToken** propriedade escolhendo o sinal de adição (![TreeView adição](../sharepoint/media/plus.gif "TreeView adição")) ao lado dele.  
  
8.  Escolha a seta suspensa na **OwnerActivityName** sub propriedade e, em seguida, defina as *Workflow1* valor.  
  
9. Escolha o **TaskId** propriedade e, em seguida, escolha as reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) botão para exibir o **Associar propriedade** caixa de diálogo.  
  
10. Escolha o **associar a um novo membro** guia, escolha o **criar campo** botão de opção e, em seguida, escolha o **Okey** botão.  
  
11. Escolha o **TaskProperties** propriedade e, em seguida, escolha as reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) botão para exibir o  **Associar a propriedade** caixa de diálogo.  
  
12. Escolha o **associar a um novo membro** guia, escolha o **criar campo** botão de opção e, em seguida, escolha o **Okey** botão.  
  
13. No **caixa de ferramentas**, expanda o **fluxo de trabalho do SharePoint** nó e localize o **LogToHistoryListActivity** atividade.  
  
14. Adicione esta atividade ao fluxo de trabalho executando uma das seguintes etapas:  
  
    -   Abra o menu de atalho para o **LogToHistoryListActivity** atividade, escolha **cópia**, abra o menu de atalho para o outro **soltar atividades aqui** área dentro do **IfElseActivity1** no designer de fluxo de trabalho e, em seguida, escolha **colar**.  
  
    -   Arraste o **LogToHistoryListActivity** atividade da **caixa de ferramentas**e solte-a outra **soltar atividades aqui** área dentro **IfElseActivity1** .  
  
## <a name="add-code-to-the-workflow"></a>Adicione código para o fluxo de trabalho
 Em seguida, adicione código para o fluxo de trabalho para fornecer funcionalidade ele.  
  
#### <a name="to-add-code-to-the-workflow"></a>Adicionar código para o fluxo de trabalho  
  
1.  Abra o menu de atalho para o **createTask1** atividade no designer de fluxo de trabalho e, em seguida, escolha **Exibir código**.  
  
2.  Adicione o seguinte método:  
  
    ```vb  
    Private Sub createTask1_MethodInvoking(ByVal sender As   
      System.Object, ByVal e As System.EventArgs)  
        createTask1_TaskId1 = Guid.NewGuid  
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser"  
        createTask1_TaskProperties1.Description = "Please approve the   
          expense report"  
        createTask1_TaskProperties1.Title = "Expense Report Approval   
          Needed"  
    End Sub   
    ```  
  
    ```csharp  
    private void createTask1_MethodInvoking(object sender, EventArgs e)  
    {  
        createTask1_TaskId1 = Guid.NewGuid();  
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser";  
        createTask1_TaskProperties1.Description = "Please approve the   
          expense report";  
        createTask1_TaskProperties1.Title = "Expense Report Approval   
          Needed";  
    }   
    ```  
  
    > [!NOTE]  
    >  No código, substitua `somedomain\\someuser` com um nome de usuário e domínio para o qual uma tarefa será criada, por exemplo, "`Office\\JoeSch`". Para testar é mais fácil de usar a conta que você está desenvolvendo com.  
  
3.  Abaixo de `MethodInvoking` método, adicione o exemplo a seguir:  
  
    ```vb  
    Private Sub checkApprovalNeeded(ByVal sender As Object, ByVal e As   
      ConditionalEventArgs)  
        Dim approval As Boolean = False  
        If (Convert.ToInt32(workflowProperties.InitiationData) >   
          Convert.ToInt32(workflowProperties.AssociationData)) Then  
            approval = True  
        End If  
        e.Result = approval  
    End Sub   
    ```  
  
    ```csharp  
    private void checkApprovalNeeded(object sender, ConditionalEventArgs   
      e)  
    {  
        bool approval = false;  
        if (Convert.ToInt32(workflowProperties.InitiationData) >   
          Convert.ToInt32(workflowProperties.AssociationData))  
        {  
            approval = true;  
        }  
        e.Result = approval;  
    }   
    ```  
  
4.  No designer de fluxo de trabalho, escolha o **ifElseBranchActivity1** atividade.  
  
5.  No **propriedades** janela, escolha a seta suspensa do **condição** propriedade e, em seguida, defina a *condição de código* valor.  
  
6.  Expanda o **condição** propriedade escolhendo o sinal de adição (![TreeView adição](../sharepoint/media/plus.gif "TreeView adição")) ao lado dele e, em seguida, defina seu valor como *checkApprovalNeeded* .  
  
7.  No designer de fluxo de trabalho, abra o menu de atalho para o **logToHistoryListActivity1** atividade e, em seguida, escolha **gerar manipuladores** para gerar um método vazio para o `MethodInvoking` eventos.  
  
8.  Substitua o `MethodInvoking` código com o seguinte:  
  
    ```vb  
    Private Sub logToHistoryListActivity1_MethodInvoking(ByVal sender As   
      System.Object, ByVal e As System.EventArgs)  
        Me.logToHistoryListActivity1.HistoryOutcome = ("Expense was auto   
          approved for " + workflowProperties.InitiationData)  
    End Sub   
    ```  
  
    ```csharp  
    private void logToHistoryListActivity1_MethodInvoking(object sender,   
      EventArgs e)  
    {  
        this.logToHistoryListActivity1.HistoryOutcome = "Expense was   
          auto approved for " + workflowProperties.InitiationData;  
    }   
    ```  
  
9. Escolha o **F5** chave para depurar o programa.  
  
     Isso compila o aplicativo clicar, um pacote, implanta, ativa seus recursos, recicla o [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] pool de aplicativos e, em seguida, inicia o navegador no local especificado na **Url do Site** propriedade.  
  
## <a name="associating-the-workflow-to-the-documents-list"></a>Associar o fluxo de trabalho à lista de documentos
 Em seguida, exibir o formulário de associação de fluxo de trabalho por meio da associação de fluxo de trabalho com o **SharedDocuments** lista no site do SharePoint.  
  
#### <a name="to-associate-the-workflow"></a>Para associar o fluxo de trabalho  
  
1.  Escolha o **documentos compartilhados** link na barra de início rápido.  
  
2.  Escolha o **biblioteca** no link a **ferramentas de biblioteca** guia e, em seguida, escolha o **configurações da biblioteca** botão faixa de opções.  
  
3.  No **permissões e gerenciamento** , escolha o **configurações de fluxo de trabalho** vincular e, em seguida, escolha o **adicionar um fluxo de trabalho** no link a **defluxosdetrabalho** página.  
  
4.  Na lista superior na página de configurações do fluxo de trabalho, escolha o **ExpenseReport - Workflow1** modelo.  
  
5.  No próximo campo, insira **ExpenseReportWorkflow** e, em seguida, escolha o **próxima** botão.  
  
     Isso associa o fluxo de trabalho com o **documentos compartilhados** listar e exibe o formulário de associação de fluxo de trabalho.  
  
6.  No **limite de aprovação automática** texto, digite **1200** e, em seguida, escolha o **associar o fluxo de trabalho** botão.  
  
## <a name="start-the-workflow"></a>Iniciar o fluxo de trabalho
 Em seguida, associar o fluxo de trabalho para um dos documentos na **documentos compartilhados** lista para exibir o formulário de iniciação do fluxo de trabalho.  
  
#### <a name="to-start-the-workflow"></a>Para iniciar o fluxo de trabalho  
  
1.  Na página do SharePoint, escolha o **Home** botão.  
  
2.  Escolha o **documentos compartilhados** link na barra QuickLaunch para exibir o **documentos compartilhados** lista.  
  
3.  Escolha o **documentos** no link a **ferramentas de biblioteca** guia na parte superior da página e, em seguida, escolha o **carregar documento** botão na faixa de opções para carregar um novo documento no **Documentos compartilhados** lista.  
  
4.  No **carregar documento** caixa de diálogo, escolha o **procurar** botão, escolha qualquer arquivo de documento, escolha o **abrir** botão e, em seguida, escolha o **Okey** botão.  
  
     Você pode alterar as configurações para o documento na caixa de diálogo, mas deixá-los com os valores padrão ao escolher o **salvar** botão.  
  
5.  Escolha o documento carregado, clique na seta suspensa que aparece e, em seguida, escolha o **fluxos de trabalho** item.  
  
6.  Escolha a imagem ao lado de ExpenseReportWorkflow.  
  
     Isso exibe o formulário de iniciação do fluxo de trabalho. (Observe que o valor exibido na **limite de aprovação automática** caixa é somente leitura porque ele foi inserido no formulário de associação.)  
  
7.  No **Total de despesa** texto, digite **1600**e, em seguida, escolha o **Iniciar fluxo de trabalho** botão.  
  
     Isso exibe a **documentos compartilhados** lista novamente. Uma nova coluna chamada **ExpenseReportWorkflow** com o valor **concluído** é adicionada ao item de apenas usar o fluxo de trabalho.  
  
8.  Escolha a seta suspensa ao lado do documento carregado e, em seguida, escolha o **fluxos de trabalho** item para exibir a página de status do fluxo de trabalho. Escolha o **Completed** valor sob **fluxos de trabalho concluído**. A tarefa está listada sob o **tarefas** seção.  
  
9. Escolha o título da tarefa para exibir seus detalhes de tarefa.  
  
10. Volte para o **SharedDocuments** listar e reinicie o fluxo de trabalho, usando o mesmo documento ou um diferente.  
  
11. Insira um valor na página de início é menor que ou igual ao valor inserido na página associação (**1200**).  
  
     Quando isso ocorre, uma entrada na lista de histórico é criada em vez de uma tarefa. A entrada exibida na **histórico de fluxo de trabalho** seção da página de status do fluxo de trabalho. Observe a mensagem na **resultado** coluna do evento do histórico. Ele contém o texto inserido no `logToHistoryListActivity1.MethodInvoking` evento, que inclui a quantidade que foi aprovada automaticamente.  
  
## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar modelos de fluxo de trabalho a partir destes tópicos:  
  
-   Para saber mais sobre fluxos de trabalho do SharePoint, consulte [fluxos de trabalho no Windows SharePoint Services](http://go.microsoft.com/fwlink/?LinkID=166275).  
  
## <a name="see-also"></a>Consulte também
 [Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)   
 [Passo a passo: Adicionar uma página de aplicativo a um fluxo de trabalho](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)  
  
