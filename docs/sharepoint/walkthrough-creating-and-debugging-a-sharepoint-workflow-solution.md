---
title: Criar & solução de fluxo de trabalho do SharePoint de depuração
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65af3cbfc799a90d640579f8eed0e051fd5888f0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014624"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>Walkthrough: criar e depurar uma solução de fluxo de trabalho do SharePoint
  Este tutorial demonstra como criar um modelo de fluxo de trabalho seqüencial básico. O fluxo de trabalho verifica uma propriedade de uma biblioteca de documentos compartilhada para determinar se um documento foi revisado. Se o documento tiver sido revisado, o fluxo de trabalho é concluído.

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de fluxo de trabalho Sequencial de definição de lista do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

- Criando atividades de fluxo de trabalho.

- Manipulação de eventos de atividade de fluxo de trabalho.

> [!NOTE]
> Embora este passo a passos use um projeto de fluxo de trabalho Sequencial, o processo é idêntico para um projeto de fluxo de trabalho de máquina de estado.
>
> Além disso, o computador pode mostrar diferentes nomes ou locais para alguns dos elementos da interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio.

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>Adicionar propriedades à biblioteca de documentos compartilhados do SharePoint
 Para acompanhar o status de revisão dos documentos na biblioteca de **documentos compartilhados** , criaremos três novas propriedades para documentos compartilhados em nosso site do SharePoint: `Status` , `Assignee` e `Review Comments` . Definimos essas propriedades na biblioteca de **documentos compartilhados** .

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>Para adicionar propriedades à biblioteca de documentos compartilhados do SharePoint

1. Abra um site do SharePoint, como http:// \<system name> /SitePages/Home.aspx, em um navegador da Web.

2. Na barra de início rápido, escolha **SharedDocuments**.

3. Escolha **biblioteca** na faixa de seleção **ferramentas de biblioteca** e, em seguida, escolha o botão **criar coluna** na faixa de faixas para criar uma nova coluna.

4. Nomeie a coluna **status do documento**, defina seu tipo como **Choice (menu para escolher)**, especifique as três opções a seguir e, em seguida, escolha o botão **OK** :

    - **Revisão necessária**

    - **Revisão concluída**

    - **Alterações solicitadas**

5. Crie mais duas colunas e nomeie-as como **atribuir** e **revisar comentários**. Defina o tipo de coluna de atribuição como uma única linha de texto e o tipo de coluna comentários de revisão como várias linhas de texto.

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>Habilitar documentos a serem editados sem a necessidade de um check-out
 É mais fácil testar o modelo de fluxo de trabalho quando você pode editar os documentos sem precisar verificá-los. No próximo procedimento, você configura o site do SharePoint para habilitá-lo.

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>Para permitir que os documentos sejam editados sem verificá-los

1. Na barra de início rápido, escolha o link **documentos compartilhados** .

2. Na faixa de opções **ferramentas de biblioteca** , escolha a guia **biblioteca** e, em seguida, escolha o botão **configurações da biblioteca** para exibir a página Configurações da **biblioteca de documentos** .

3. Na seção **configurações gerais** , escolha o link **configurações de controle de versão** para exibir a página de **configurações de controle de versão** .

4. Verifique se a configuração para **exigir que os documentos sejam verificados antes que possam ser editadas** é **não**. Se não estiver, altere-o para **não** e, em seguida, escolha o botão **OK** .

5. Feche o navegador.

## <a name="create-a-sharepoint-sequential-workflow-project"></a>Criar um projeto de fluxo de trabalho Sequencial do SharePoint
 Um fluxo de trabalho Sequencial é um conjunto de etapas executadas na ordem até que a última atividade seja concluída. Neste procedimento, criamos um fluxo de trabalho Sequencial que será aplicado à nossa lista de documentos compartilhados. O assistente de fluxo de trabalho permite associar o fluxo de trabalho à definição de site ou à definição de lista e permite que você determine quando o fluxo de trabalho será iniciado.

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>Para criar um projeto de fluxo de trabalho Sequencial do SharePoint

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

3. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

4. No painel **modelos** , escolha o modelo de **projeto do SharePoint 2010** .

5. Na caixa **nome** , digite **MySharePointWorkflow** e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido.

6. Na página **especificar o site e o nível de segurança para depuração** , escolha o botão de opção **implantar como uma solução de farm** e escolha o botão **concluir** para aceitar o nível de confiança e o site padrão.

     Esta etapa define o nível de confiança para a solução como solução de farm, a única opção disponível para projetos de fluxo de trabalho. Para obter mais informações, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7. Em **Gerenciador de soluções**, escolha o nó do projeto e, na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

8. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o nó **2010** .

9. No painel **modelos** , escolha o modelo **fluxo de trabalho Sequencial (somente solução de farm)** e, em seguida, escolha o botão **Adicionar** .

     O **Assistente para personalização do SharePoint** é exibido.

10. Na página **especificar o nome do fluxo de trabalho para depuração** , aceite o nome padrão (**MySharePointWorkflow-Workflow1**). Mantenha o valor do tipo de modelo de fluxo de trabalho padrão, **lista fluxo de trabalho**e, em seguida, escolha o botão **Avançar** .

11. Na página **você gostaria que o Visual Studio associasse automaticamente o fluxo de trabalho em uma sessão de depuração?** , escolha o botão **Avançar** para aceitar todas as configurações padrão.

     Esta etapa associa automaticamente o fluxo de trabalho à biblioteca de documentos compartilhados.

12. Na página **especificar as condições de como o fluxo de trabalho é iniciado** , deixe as opções padrão selecionadas na seção **como você deseja que o fluxo de trabalho seja iniciado?** e escolha o botão **concluir** .

     Esta página permite que você especifique quando o fluxo de trabalho é iniciado. Por padrão, o fluxo de trabalho é iniciado quando um usuário o inicia manualmente no SharePoint ou quando um item ao qual o fluxo de trabalho está associado é criado.

## <a name="create-workflow-activities"></a>Criar atividades de fluxo de trabalho
 Os fluxos de trabalho contêm uma ou mais *atividades* que representam ações a serem executadas. Use o designer de fluxo de trabalho para organizar as atividades de um fluxo de trabalho. Neste procedimento, adicionaremos duas atividades ao fluxo de trabalho: HandleExternalEventActivity e OnWorkFlowItemChanged. Essas atividades monitoram o status da revisão de documentos na lista de **documentos compartilhados**

#### <a name="to-create-workflow-activities"></a>Para criar atividades de fluxo de trabalho

1. O fluxo de trabalho deve ser exibido no designer de fluxo de trabalho. Se não estiver, abra **Workflow1.cs** ou **Workflow1. vb** no **Gerenciador de soluções**.

2. No designer, escolha a atividade **OnWorkflowActivated1** .

3. Na janela **Propriedades** , digite **OnWorkflowActivated** ao lado da propriedade **invocada** e escolha a tecla Enter.

     O editor de código é aberto e um método de manipulador de eventos chamado onWorkflowActivated é adicionado ao arquivo de código Workflow1.

4. Volte para o designer de fluxo de trabalho, abra a caixa de ferramentas e, em seguida, expanda o nó **Windows Workflow v 3.0** .

5. No nó **Windows Workflow v 3.0** da caixa de **ferramentas**, execute um dos seguintes conjuntos de etapas:

    1. Abra o menu de atalho para a atividade **while** e, em seguida, escolha **copiar**. No designer de fluxo de trabalho, abra o menu de atalho da linha sob a atividade **OnWorkflowActivated1** e escolha **colar**.

    2. Arraste a atividade **while** da **caixa de ferramentas** para o designer de fluxo de trabalho e conecte a atividade à linha sob a atividade **OnWorkflowActivated1** .

6. Escolha a atividade **whileActivity1** .

7. Na janela **Propriedades** , defina **condição** como condição de código.

8. Expanda a propriedade **condição** , digite **isWorkflowPending** ao lado da propriedade **condição** filho e, em seguida, escolha a tecla Enter.

     O editor de código é aberto e um método chamado isWorkflowPending é adicionado ao arquivo de código Workflow1.

9. Volte para o designer de fluxo de trabalho, abra a caixa de ferramentas e, em seguida, expanda o nó **fluxo de trabalho do SharePoint** .

10. No nó **fluxo de trabalho do SharePoint** da **caixa de ferramentas**, execute um dos seguintes conjuntos de etapas:

    - Abra o menu de atalho para a atividade **OnWorkflowItemChanged** e escolha **copiar**. No designer de fluxo de trabalho, abra o menu de atalho da linha dentro da atividade **whileActivity1** e escolha **colar**.

    - Arraste a atividade **OnWorkflowItemChanged** da **caixa de ferramentas** para o designer de fluxo de trabalho e conecte a atividade à linha dentro da atividade **whileActivity1** .

11. Escolha a atividade **onWorkflowItemChanged1** .

12. Na janela **Propriedades** , defina as propriedades conforme mostrado na tabela a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**Invocado**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>Manipular eventos de atividade
 Por fim, verifique o status do documento de cada atividade. Se o documento tiver sido revisado, o fluxo de trabalho será concluído.

#### <a name="to-handle-activity-events"></a>Para lidar com eventos de atividade

1. Em *Workflow1.cs* ou *Workflow1. vb*, adicione o campo a seguir à parte superior da `Workflow1` classe. Esse campo é usado em uma atividade para determinar se o fluxo de trabalho foi concluído.

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. Adicione o método a seguir à classe `Workflow1`. Esse método verifica o valor da `Document Status` propriedade da lista de documentos para determinar se o documento foi revisado. Se a `Document Status` propriedade for definida como `Review Complete` , o `checkStatus` método definirá o `workflowPending` campo como **false** para indicar que o fluxo de trabalho está pronto para ser concluído.

    ```vb
    Private Sub checkStatus()
        If CStr(workflowProperties.Item("Document Status")) = "Review Complete" Then
            workflowPending = False
        End If
    End Sub
    ```

    ```csharp
    private void checkStatus()
    {
        if ((string)workflowProperties.Item["Document Status"] == "Review Complete")
        workflowPending = false;
    }
    ```

3. Adicione o código a seguir aos `onWorkflowActivated` `onWorkflowItemChanged` métodos e para chamar o `checkStatus` método. Quando o fluxo de trabalho é iniciado, o `onWorkflowActivated` método chama o `checkStatus` método para determinar se o documento já foi revisado. Se ele não tiver sido revisado, o fluxo de trabalho continuará. Quando o documento é salvo, o `onWorkflowItemChanged` método chama o `checkStatus` método novamente para determinar se o documento foi revisado. Enquanto o `workflowPending` campo está definido como **true**, o fluxo de trabalho continua a ser executado.

    ```vb
    Private Sub onWorkflowActivated(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub

    Private Sub onWorkflowItemChanged(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub
    ```

    ```csharp
    private void onWorkflowActivated(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }

    private void onWorkflowItemChanged(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }
    ```

4. Adicione o código a seguir ao `isWorkflowPending` método para verificar o status da `workflowPending` propriedade. Cada vez que o documento é salvo, a atividade **whileActivity1** chama o `isWorkflowPending` método. Esse método examina a <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> Propriedade do <xref:System.Workflow.Activities.ConditionalEventArgs> objeto para determinar se a atividade **whileActivity1** deve continuar ou terminar. Se a propriedade for definida como **true**, a atividade continuará. Caso contrário, a atividade será concluída e o fluxo de trabalho será concluído.

    ```vb
    Private Sub isWorkflowPending(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ConditionalEventArgs)
        e.Result = workflowPending
    End Sub
    ```

    ```csharp
    private void isWorkflowPending(object sender, ConditionalEventArgs e)
    {
        e.Result = workflowPending;
    }
    ```

5. Salve o projeto.

## <a name="test-the-sharepoint-workflow-template"></a>Testar o modelo de fluxo de trabalho do SharePoint
 Quando você inicia o depurador, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o implanta o modelo de fluxo de trabalho no servidor do SharePoint e associa o fluxo de trabalho à lista de **documentos compartilhados** . Para testar o fluxo de trabalho, inicie uma instância do fluxo de trabalho de um documento na lista **documentos compartilhados** .

#### <a name="to-test-the-sharepoint-workflow-template"></a>Para testar o modelo de fluxo de trabalho do SharePoint

1. Em *Workflow1.cs* ou *Workflow1. vb*, defina um ponto de interrupção ao lado do método **OnWorkflowActivated** .

2. Escolha a tecla **F5** para compilar e executar a solução.

     O site do SharePoint é exibido.

3. No painel de navegação do SharePoint, escolha o link **documentos compartilhados** .

4. Na página **documentos compartilhados** , escolha o link **documentos** na guia **ferramentas de biblioteca** e, em seguida, escolha o botão **carregar documento** .

5. Na caixa de diálogo **carregar documento** , escolha o botão **procurar** , escolha qualquer arquivo de documento, escolha o botão **abrir** e, em seguida, escolha o botão **OK** .

     Isso carrega o documento selecionado na lista **documentos compartilhados** e inicia o fluxo de trabalho.

6. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , verifique se o depurador para no ponto de interrupção ao lado do `onWorkflowActivated` método.

7. Escolha a tecla **F5** para continuar a execução.

8. Você pode alterar as configurações do documento aqui, mas deixá-las com os valores padrão por enquanto, escolhendo o botão **salvar** .

     Isso retorna para a página **documentos compartilhados** do site padrão do SharePoint.

9. Na página **documentos compartilhados** , verifique se o valor abaixo da coluna **MySharePointWorkflow-Workflow1** está definido como **em andamento**. Isso indica que o fluxo de trabalho está em andamento e que o documento está aguardando revisão.

10. Na página **documentos compartilhados** , escolha o documento, escolha a seta que aparece e, em seguida, escolha o item de menu **Editar propriedades** .

11. Defina **status do documento** como **revisão completa**e, em seguida, escolha o botão **salvar** .

     Isso retorna para a página **documentos compartilhados** do site padrão do SharePoint.

12. Na página **documentos compartilhados** , verifique se o valor abaixo da coluna **status do documento** está definido como **revisão concluída**. Atualize a página **documentos compartilhados** e verifique se o valor abaixo da coluna **MySharePointWorkflow-Workflow1** está definido como **concluído**. Isso indica que o fluxo de trabalho foi concluído e que o documento foi revisado.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar modelos de fluxo de trabalho a partir destes tópicos:

- Para saber mais sobre as atividades de fluxo de trabalho do SharePoint, veja [atividades de fluxo de trabalho do SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14)).

- Para saber mais sobre Windows Workflow Foundation atividades, consulte [namespace System. Workflow. Activities](/dotnet/api/system.windows.media.color).

## <a name="see-also"></a>Consulte também
- [Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [Modelos de projeto e item de projeto do SharePoint](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
