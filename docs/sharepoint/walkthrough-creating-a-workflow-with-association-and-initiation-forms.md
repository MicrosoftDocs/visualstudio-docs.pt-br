---
title: Criar fluxo de trabalho com formulários de associação e de inicialização
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6f257dfed2fe439c5ab22ab9951b6258116c6567
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017128"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização
  Este tutorial demonstra como criar um fluxo de trabalho seqüencial básico que incorpora o uso de associação e formulários de inicialização. Esses são formulários ASPX que permitem que os parâmetros sejam adicionados a um fluxo de trabalho quando ele é associado pela primeira vez pelo administrador do SharePoint (o formulário de associação) e quando o fluxo de trabalho é iniciado pelo usuário (o formulário de inicialização).

 Este passo a passos descreve um cenário em que um usuário deseja criar um fluxo de trabalho de aprovação para relatórios de despesas com os seguintes requisitos:

- Quando o fluxo de trabalho é associado a uma lista, o administrador recebe um formulário de associação onde insere um limite de dólar para relatórios de despesas.

- Os funcionários carregam seus relatórios de despesas na lista de documentos compartilhados, iniciam o fluxo de trabalho e, em seguida, inserem o total de despesas no formulário de inicialização do fluxo de trabalho.

- Se o total de um relatório de despesas do funcionário exceder o limite predefinido do administrador, uma tarefa será criada para o gerente do funcionário aprovar o relatório de despesas. No entanto, se o total do relatório de despesas de um funcionário for menor ou igual ao limite de despesas, uma mensagem aprovada automaticamente será gravada na lista de histórico do fluxo de trabalho.

  Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de fluxo de trabalho Sequencial de definição de lista do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

- Criando um agendamento de fluxo de trabalho.

- Manipulação de eventos de atividade de fluxo de trabalho.

- Criando formulários de associação e inicialização de fluxo de trabalho.

- Associando o fluxo de trabalho.

- Iniciando o fluxo de trabalho manualmente.

> [!NOTE]
> Embora este passo a passos use um projeto de fluxo de trabalho Sequencial, o processo é o mesmo para fluxos de trabalho de máquina de estado.
>
> Além disso, o computador pode mostrar diferentes nomes ou locais para alguns dos [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] elementos da interface do usuário nas instruções a seguir. A [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] edição que você tem e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

## <a name="create-a-sharepoint-sequential-workflow-project"></a>Criar um projeto de fluxo de trabalho Sequencial do SharePoint
 Primeiro, crie um projeto de fluxo de trabalho Sequencial no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Um fluxo de trabalho Sequencial é uma série de etapas executadas em ordem até que a última atividade seja concluída. Neste procedimento, você criará um fluxo de trabalho Sequencial que se aplica à lista de documentos compartilhados no SharePoint. O assistente do fluxo de trabalho permite associar o fluxo de trabalho ao site ou à definição de lista e permite que você determine quando o fluxo de trabalho será iniciado.

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>Para criar um projeto de fluxo de trabalho Sequencial do SharePoint

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. No painel **modelos** , escolha o modelo projeto de **projeto do SharePoint 2010** .

4. Na caixa **nome** , digite **ExpenseReport** e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido.

5. Na página **especificar o site e o nível de segurança para depuração** , escolha o botão de opção **implantar como uma solução de farm** e escolha o botão **concluir** para aceitar o nível de confiança e o site padrão.

     Essa etapa também define o nível de confiança para a solução como solução de farm, que é a única opção disponível para projetos de fluxo de trabalho.

6. Em **Gerenciador de soluções**, escolha o nó do projeto.

7. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

8. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o nó **2010** .

9. No painel **modelos** , escolha o modelo **fluxo de trabalho Sequencial (somente solução de farm)** e, em seguida, escolha o botão **Adicionar** .

     O **Assistente para personalização do SharePoint** é exibido.

10. Na página **especificar o nome do fluxo de trabalho para depuração** , aceite o nome padrão (**ExpenseReport-Workflow1**). Mantenha o valor do tipo de modelo de fluxo de trabalho padrão (**listar fluxo de trabalho)**. Escolha o botão **Avançar**.

11. Na página **você gostaria que o Visual Studio associasse automaticamente o fluxo de trabalho em uma sessão de depuração?** , desmarque a caixa que associará automaticamente seu modelo de fluxo de trabalho, caso ele esteja marcado.

     Esta etapa permite que você associe manualmente o fluxo de trabalho com a lista de documentos compartilhados posteriormente, que exibe o formulário associação.

12. Escolha o botão **Concluir**.

## <a name="add-an-association-form-to-the-workflow"></a>Adicionar um formulário de associação ao fluxo de trabalho
 Em seguida, crie um. Formulário de associação ASPX que aparece quando o administrador do SharePoint primeiro associa o fluxo de trabalho a um documento de relatório de despesas.

#### <a name="to-add-an-association-form-to-the-workflow"></a>Para adicionar um formulário de associação ao fluxo de trabalho

1. Escolha o nó **Workflow1** em **Gerenciador de soluções**.

2. Na barra de menus, escolha **projeto**  >  **Adicionar novo item** para exibir a caixa de diálogo **Adicionar novo item** .

3. Na exibição de árvore da caixa de diálogo, expanda **Visual C#** ou **Visual Basic** (dependendo da linguagem do seu projeto), expanda o nó do **SharePoint** e escolha o nó **2010** .

4. Na lista de modelos, escolha o modelo de **formulário Associação de fluxo de trabalho** .

5. Na caixa de texto **nome** , digite **ExpenseReportAssocForm. aspx**.

6. Escolha o botão **Adicionar** para adicionar o formulário ao projeto.

## <a name="designing-and-coding-the-association-form"></a>Criando e codificando o formulário de associação
 Neste procedimento, você introduz a funcionalidade para o formulário de associação adicionando controles e código a ele.

#### <a name="to-design-and-code-the-association-form"></a>Para criar e codificar o formulário de associação

1. No formulário associação (ExpenseReportAssocForm. aspx), localize o `asp:Content` elemento que tem `ID="Main"` .

2. Diretamente após a primeira linha nesse elemento de conteúdo, adicione o seguinte código para criar um rótulo e uma caixa de texto que solicite o limite de aprovação de despesas (*AutoApproveLimit*):

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. Expanda o arquivo **ExpenseReportAssocForm. aspx** em **Gerenciador de soluções** para exibir seus arquivos dependentes.

    > [!NOTE]
    > Se o seu projeto estiver no [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] , você deverá escolher o botão **Exibir todos os arquivos** para executar essa etapa.

4. Abra o menu de atalho para o arquivo ExpenseReportAssocForm. aspx e escolha **Exibir código**.

5. Substitua o `GetAssociationData` método por:

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

## <a name="add-an-initiation-form-to-the-workflow"></a>Adicionar um formulário de inicialização ao fluxo de trabalho
 Em seguida, crie o formulário de inicialização que aparece quando os usuários executam o fluxo de trabalho em seus relatórios de despesas.

#### <a name="to-create-an-initiation-form"></a>Para criar um formulário de inicialização

1. Escolha o nó **Workflow1** em **Gerenciador de soluções**.

2. Na barra de menus, escolha **projeto**  >  **Adicionar novo item** exibir a caixa de diálogo **Adicionar novo item** .

3. Na exibição de árvore da caixa de diálogo, expanda **Visual C#** ou **Visual Basic** (dependendo da linguagem do seu projeto), expanda o nó do **SharePoint** e escolha o nó **2010** .

4. Na lista de modelos, escolha o modelo **formulário de inicialização do fluxo de trabalho** .

5. Na caixa de texto **nome** , digite **ExpenseReportInitForm. aspx**.

6. Escolha o botão **Adicionar** para adicionar o formulário ao projeto.

## <a name="designing-and-coding-the-initiation-form"></a>Criando e codificando o formulário de inicialização
 Em seguida, introduza a funcionalidade para o formulário de inicialização adicionando controles e código a ele.

#### <a name="to-code-the-initiation-form"></a>Para codificar o formulário de inicialização

1. No formulário de inicialização (ExpenseReportInitForm. aspx), localize o `asp:Content` elemento que contém `ID="Main"` .

2. Diretamente após a primeira linha nesse elemento de conteúdo, adicione o código a seguir para criar um rótulo e uma caixa de texto que exibe o limite de aprovação de despesa (*AutoApproveLimit*) que foi inserido no formulário de associação e outro rótulo e caixa de texto para solicitar o total de despesas (*ExpenseTotal*):

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. Expanda o arquivo **ExpenseReportInitForm. aspx** em **Gerenciador de soluções** para exibir seus arquivos dependentes.

4. Abra o menu de atalho para o arquivo ExpenseReportInitForm. aspx e escolha **Exibir código**.

5. Substitua o `Page_Load` método pelo exemplo a seguir:

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

6. Substitua o `GetInitiationData` método pelo exemplo a seguir:

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

## <a name="cutomize-the-workflow"></a>Cutomize o fluxo de trabalho
 Em seguida, personalize o fluxo de trabalho. Posteriormente, você associará dois formulários ao fluxo de trabalho.

#### <a name="to-customize-the-workflow"></a>Para personalizar o fluxo de trabalho

1. Exiba o fluxo de trabalho no designer de fluxo de trabalho abrindo Workflow1 no projeto.

2. Na **caixa de ferramentas**, expanda o nó **Windows Workflow v 3.0** e localize a atividade **IfElse** .

3. Adicione essa atividade ao fluxo de trabalho executando uma das seguintes etapas:

    - Abra o menu de atalho para a atividade **IfElse** , escolha **copiar**, abra o menu de atalho da linha sob a atividade **OnWorkflowActivated1** no designer de fluxo de trabalho e escolha **colar**.

    - Arraste a atividade **IfElse** da **caixa de ferramentas**e conecte-a à linha sob a atividade **onWorkflowActiviated1** no designer de fluxo de trabalho.

4. Na caixa de ferramentas, expanda o nó **fluxo de trabalho do SharePoint** e localize a atividade **CreateTask** .

5. Adicione essa atividade ao fluxo de trabalho executando uma das seguintes etapas:

    - Abra o menu de atalho para a atividade **CreateTask** , escolha **copiar**, abra o menu de atalho de uma das duas **atividades soltar aqui** áreas dentro de **IfElseActivity1** no designer de fluxo de trabalho e escolha **colar**.

    - Arraste a atividade **CreateTask** da **caixa de ferramentas** para uma das duas **atividades soltar aqui** nas áreas do **IfElseActivity1**.

6. Na janela **Propriedades** , insira um valor de propriedade de *taskToken* para a propriedade **CorrelationToken** .

7. Expanda a propriedade **CorrelationToken** escolhendo o sinal de adição (![TreeView Plus](../sharepoint/media/plus.gif "TreeView Plus")) ao lado dele.

8. Escolha a seta suspensa na subpropriedade **OwnerActivityName** e defina o valor *Workflow1* .

9. Escolha a propriedade **TaskId** e escolha o botão de reticências (![ASP.NET Mobile Designer Ellipse](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) para exibir a caixa de diálogo **propriedade de associação** .

10. Escolha a guia **associar a um novo membro** , escolha o botão de opção **criar campo** e, em seguida, escolha o botão **OK** .

11. escolha a propriedade **TaskProperties** e escolha o botão de reticências (![ASP.NET Mobile Designer Ellipse](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) para exibir a caixa de diálogo **propriedade de associação** .

12. Escolha a guia **associar a um novo membro** , escolha o botão de opção **criar campo** e, em seguida, escolha o botão **OK** .

13. Na **caixa de ferramentas**, expanda o nó fluxo de **trabalho do SharePoint** e localize a atividade **LogToHistoryListActivity** .

14. Adicione essa atividade ao fluxo de trabalho executando uma das seguintes etapas:

    - Abra o menu de atalho para a atividade **LogToHistoryListActivity** , escolha **copiar**, abra o menu de atalho para as outras **atividades soltar aqui** na área de **IfElseActivity1** no designer de fluxo de trabalho e escolha **colar**.

    - Arraste a atividade **LogToHistoryListActivity** da **caixa de ferramentas**e solte-a em outras **atividades soltar aqui** na área de **IfElseActivity1**.

## <a name="add-code-to-the-workflow"></a>Adicionar código ao fluxo de trabalho
 Em seguida, adicione o código ao fluxo de trabalho para fornecer a funcionalidade de ti.

#### <a name="to-add-code-to-the-workflow"></a>Para adicionar código ao fluxo de trabalho

1. Abra o menu de atalho da atividade **createTask1** no designer de fluxo de trabalho e escolha **Exibir código**.

2. Adicione o seguinte método:

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
    > No código, substitua `somedomain\\someuser` por um domínio e nome de usuário para o qual uma tarefa será criada, como " `Office\\JoeSch` ". Para teste, é mais fácil usar a conta com a qual você está desenvolvendo.

3. Abaixo do `MethodInvoking` método, adicione o seguinte exemplo:

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

4. No designer de fluxo de trabalho, escolha a atividade **ifElseBranchActivity1** .

5. Na janela **Propriedades** , escolha a seta suspensa da propriedade **condição** e, em seguida, defina o valor *condição de código* .

6. Expanda a propriedade **condição** escolhendo o sinal de adição (![TreeView Plus](../sharepoint/media/plus.gif "TreeView Plus")) ao lado dele e, em seguida, defina seu valor como *checkApprovalNeeded*.

7. No designer de fluxo de trabalho, abra o menu de atalho da atividade **logToHistoryListActivity1** e escolha **gerar manipuladores** para gerar um método vazio para o `MethodInvoking` evento.

8. Substitua o `MethodInvoking` código pelo seguinte:

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

9. Escolha a tecla **F5** para depurar o programa.

     Isso compila o aplicativo, empacota-o, implanta, ativa seus recursos, recicla o [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] pool de aplicativos e, em seguida, inicia o navegador no local especificado na propriedade **URL do site** .

## <a name="associating-the-workflow-to-the-documents-list"></a>Associando o fluxo de trabalho à lista de documentos
 Em seguida, exiba o formulário Associação de fluxo de trabalho associando o fluxo de trabalho com a lista **SharedDocuments** no site do SharePoint.

#### <a name="to-associate-the-workflow"></a>Para associar o fluxo de trabalho

1. Escolha o link **documentos compartilhados** na barra de início rápido.

2. Escolha o link **biblioteca** na guia **ferramentas de biblioteca** e, em seguida, escolha o botão de faixa de **opções configurações da biblioteca** .

3. Na seção **permissões e gerenciamento** , escolha o link **configurações de fluxo** de trabalho e escolha o link **Adicionar um fluxo de trabalho** na página **fluxos de trabalho** .

4. Na lista superior da página Configurações de fluxo de trabalho, escolha o modelo **ExpenseReport-Workflow1** .

5. No próximo campo, insira **ExpenseReportWorkflow** e, em seguida, escolha o botão **Avançar** .

     Isso associa o fluxo de trabalho à lista de **documentos compartilhados** e exibe o formulário Associação de fluxo de trabalho.

6. Na caixa de texto **limite de aprovação automática** , insira **1200** e, em seguida, escolha o botão **associar fluxo de trabalho** .

## <a name="start-the-workflow"></a>Iniciar o fluxo de trabalho
 Em seguida, associe o fluxo de trabalho a um dos documentos na lista de **documentos compartilhados** para exibir o formulário de inicialização do fluxo de trabalho.

#### <a name="to-start-the-workflow"></a>Para iniciar o fluxo de trabalho

1. Na página do SharePoint, escolha o botão **página inicial** .

2. Escolha o link **documentos compartilhados** na barra de início rápido para exibir a lista de **documentos compartilhados** .

3. Escolha o link **documentos** na guia **ferramentas de biblioteca** na parte superior da página e, em seguida, escolha o botão **carregar documento** na faixa de guia para carregar um novo documento na lista **documentos compartilhados** .

4. Na caixa de diálogo **carregar documento** , escolha o botão **procurar** , escolha qualquer arquivo de documento, escolha o botão **abrir** e, em seguida, escolha o botão **OK** .

     Você pode alterar as configurações do documento nessa caixa de diálogo, mas deixá-los com os valores padrão escolhendo o botão **salvar** .

5. Escolha o documento carregado, escolha a seta suspensa que aparece e, em seguida, escolha o item **fluxos de trabalho** .

6. Escolha a imagem ao lado de ExpenseReportWorkflow.

     Isso exibe o formulário de inicialização do fluxo de trabalho. (Observe que o valor exibido na caixa **limite de aprovação automática** é somente leitura porque foi inserido no formulário associação.)

7. Na caixa de texto **total de despesas** , digite **1600**e, em seguida, escolha o botão **Iniciar fluxo de trabalho** .

     Isso exibirá a lista de **documentos compartilhados** novamente. Uma nova coluna denominada **ExpenseReportWorkflow** com o valor **concluído** é adicionada ao item que o fluxo de trabalho acabou de iniciar.

8. Escolha a seta suspensa ao lado do documento carregado e, em seguida, escolha o item **fluxos de trabalho** para exibir a página status do fluxo de trabalho. Escolha o valor **concluído** em **fluxos de trabalho concluídos**. A tarefa é listada na seção **tarefas** .

9. Escolha o título da tarefa para exibir os detalhes da tarefa.

10. Volte para a lista **SharedDocuments** e reinicie o fluxo de trabalho, usando o mesmo documento ou outro.

11. Insira um valor na página de inicialização que seja menor ou igual ao valor inserido na página associação (**1200**).

     Quando isso ocorre, uma entrada na lista de histórico é criada em vez de uma tarefa. A entrada é exibida na seção **histórico do fluxo de trabalho** da página status do fluxo de trabalho. Observe a mensagem na coluna **resultado** do evento de histórico. Ele contém o texto inserido no `logToHistoryListActivity1.MethodInvoking` evento que inclui o valor que foi aprovado automaticamente.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar modelos de fluxo de trabalho a partir destes tópicos:

- Para saber mais sobre os fluxos de trabalho do SharePoint, consulte [fluxos de trabalho no Windows SharePoint Services](/previous-versions/office/developer/sharepoint-2010/ms416312(v=office.14)).

## <a name="see-also"></a>Consulte também
- [Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [Walkthrough: adicionar uma página de aplicativo a um fluxo de trabalho](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)
