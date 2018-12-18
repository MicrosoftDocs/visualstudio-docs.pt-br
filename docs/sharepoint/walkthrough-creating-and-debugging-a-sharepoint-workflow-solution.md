---
title: 'Passo a passo: Criando e depurando uma solução de fluxo de trabalho do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c254f6f3e044f938ed2749567d66ee7a313081e7
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42626482"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>Passo a passo: Criar e depurar uma solução de fluxo de trabalho do SharePoint
  Este passo a passo demonstra como criar um modelo de fluxo de trabalho sequencial básico. O fluxo de trabalho verifica uma propriedade de uma biblioteca de documentos compartilhados para determinar se um documento foi revisado. Se o documento foi revisado, o fluxo de trabalho é concluído.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Criando um projeto de fluxo de trabalho sequencial de definição de lista do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
-   Criando atividades de fluxo de trabalho.  
  
-   Manipulação de eventos de atividade de fluxo de trabalho.  
  
> [!NOTE]  
>  Embora este passo a passo usa um projeto de fluxo de trabalho sequencial, o processo é idêntico para um projeto de fluxo de trabalho de máquina de estado.  
>   
>  Além disso, seu computador pode mostrar diferentes nomes ou localizações para alguns dos usuário do Visual Studio elementos de interface nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do Microsoft Windows e do SharePoint.  
  
-   Visual Studio.  
  
## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>Adicionar propriedades à biblioteca de documentos compartilhados do SharePoint
 Para acompanhar o status de revisão de documentos na **documentos compartilhados** biblioteca, criaremos três novas propriedades para documentos compartilhados em nosso site do SharePoint: `Status`, `Assignee`, e `Review Comments`. Podemos definir essas propriedades na **documentos compartilhados** biblioteca.  
  
#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>Para adicionar propriedades ao SharePoint shared documenta a biblioteca  
  
1.  Abrir um site do SharePoint, como http://\<nome do sistema > / SitePages/Home.aspx, em um navegador da Web.  
  
2.  Na barra de início rápido, escolha **SharedDocuments**.  
  
3.  Escolher **biblioteca** sobre o **ferramentas de biblioteca** faixa de opções e, em seguida, escolha o **criar coluna** botão na faixa de opções para criar uma nova coluna.  
  
4.  Nome da coluna **Status do documento**, defina seu tipo como **opção (menu para sua escolha)**, especifique as três opções a seguir e, em seguida, escolha o **Okey** botão:  
  
    -   **Revisão necessária**  
  
    -   **Análise concluída**  
  
    -   **Alterações solicitadas**  
  
5.  Criar mais duas colunas e nomeá-los **destinatário** e **comentários de revisão**. Defina o tipo de coluna do destinatário como uma única linha de texto e o tipo de coluna de comentários de revisão como várias linhas de texto.  
  
## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>Habilitar documentos a serem editados sem a necessidade de um check-out
 É mais fácil de testar o modelo de fluxo de trabalho quando você pode editar documentos sem a necessidade de fazer check-out. No próximo procedimento, você deve configurar o site do SharePoint para habilitá-lo.  
  
#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>Para habilitar os documentos a ser editado sem check-out  
  
1.  Na barra de início rápido, escolha o **documentos compartilhados** link.  
  
2.  No **ferramentas de biblioteca** faixa de opções, escolha o **biblioteca** guia e, em seguida, escolha o **configurações da biblioteca** botão para exibir o **Document Library Settings** página.  
  
3.  No **configurações gerais** , escolha o **configurações de controle de versão** link para exibir o **configurações de controle de versão** página.  
  
4.  Verifique a configuração para **exigir que os documentos para fazer check-out antes que eles podem ser editados** é **não**. Se não estiver, altere-o para **nenhuma** e, em seguida, escolha o **Okey** botão.  
  
5.  Feche o navegador.  
  
## <a name="create-a-sharepoint-sequential-workflow-project"></a>Criar um projeto de fluxo de trabalho sequencial do SharePoint
 Um fluxo de trabalho sequencial é um conjunto de etapas que executa em ordem até que a última atividade seja concluída. Neste procedimento, criamos um fluxo de trabalho sequencial que se aplicam a nossa lista de documentos compartilhados. O Assistente de fluxo de trabalho permite associar o fluxo de trabalho com a definição de site ou a definição de lista e permite determinar quando o fluxo de trabalho será iniciado.  
  
#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>Para criar um projeto de fluxo de trabalho sequencial do SharePoint  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.  
  
3.  Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
4.  No **modelos** painel, escolha o **o projeto do SharePoint 2010** modelo.  
  
5.  No **nome** , digite **MySharePointWorkflow** e, em seguida, escolha o **Okey** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
6.  No **especificar o nível de site e segurança para depuração** , escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão para aceitar o site padrão e o nível de confiança.  
  
     Esta etapa define o nível de confiança para a solução como solução de farm, a única opção disponível para projetos de fluxo de trabalho. Para obter mais informações, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
7.  Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **Add New Item**.  
  
8.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
9. No **modelos** painel, escolha o **fluxo de trabalho sequencial (somente solução de Farm)** modelo e, em seguida, escolha o **Add** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
10. No **especifique o nome do fluxo de trabalho para depuração** página, aceite o nome padrão (**MySharePointWorkflow - Workflow1**). Mantenha o valor de tipo de modelo de fluxo de trabalho padrão, **fluxo de trabalho de lista**e, em seguida, escolha o **próxima** botão.  
  
11. No **deseja que o Visual Studio associe automaticamente o fluxo de trabalho em uma sessão de depuração?** , escolha o **próxima** botão aceitar todas as configurações padrão.  
  
     Esta etapa automaticamente associa o fluxo de trabalho com a biblioteca de documentos compartilhados.  
  
12. No **especificam as condições para como seu fluxo de trabalho é iniciado** página, deixe as opções padrão selecionadas na **como você deseja que o fluxo de trabalho para iniciar?** seção e escolha o **concluir** botão.  
  
     Esta página permite que você especifique quando o fluxo de trabalho é iniciado. Por padrão, o fluxo de trabalho começa a quando um usuário inicia manualmente no SharePoint ou quando um item ao qual o fluxo de trabalho está associado é criado.  
  
## <a name="create-workflow-activities"></a>Criar atividades de fluxo de trabalho
 Fluxos de trabalho contêm uma ou mais *atividades* que representam as ações a serem executadas. Use o designer de fluxo de trabalho para organizar as atividades para um fluxo de trabalho. Neste procedimento, adicionaremos duas atividades ao fluxo de trabalho: HandleExternalEventActivity e OnWorkFlowItemChanged. Essas atividades monitoram o status da revisão de documentos na **documentos compartilhados** lista  
  
#### <a name="to-create-workflow-activities"></a>Para criar atividades de fluxo de trabalho  
  
1.  O fluxo de trabalho deve ser exibido no designer de fluxo de trabalho. Se não for, em seguida, abra **Workflow1.cs** ou **Workflow1.vb** na **Gerenciador de soluções**.  
  
2.  No designer, escolha o **OnWorkflowActivated1** atividade.  
  
3.  No **propriedades** janela, insira **onWorkflowActivated** ao lado de **Invoked** propriedade e, em seguida, escolha a tecla Enter.  
  
     Abre o Editor de código e um método de manipulador de eventos chamado onWorkflowActivated é adicionado ao arquivo de código Workflow1.  
  
4.  Volte para o designer de fluxo de trabalho, abra a caixa de ferramentas e, em seguida, expanda o **Windows Workflow v3.0** nó.  
  
5.  No **Windows Workflow v3.0** nó do **caixa de ferramentas**, execute um dos seguintes conjuntos de etapas:  
  
    1.  Abra o menu de atalho para o **enquanto** atividade e, em seguida, escolha **cópia**. No designer de fluxo de trabalho, abra o menu de atalho para a linha sob o **onWorkflowActivated1** atividade e, em seguida, escolha **colar**.  
  
    2.  Arraste o **enquanto** atividade da **caixa de ferramentas** para o designer de fluxo de trabalho e conecte-se a atividade para a linha no **onWorkflowActivated1** atividade.  
  
6.  Escolha o **WhileActivity1** atividade.  
  
7.  No **propriedades** janela, defina **condição** a condição de código.  
  
8.  Expanda o **condição** propriedade, digite **isWorkflowPending** ao lado do filho **condição** propriedade e, em seguida, escolha a tecla Enter.  
  
     Abre o Editor de código e um método chamado isWorkflowPending é adicionado ao arquivo de código Workflow1.  
  
9. Volte para o designer de fluxo de trabalho, abra a caixa de ferramentas e, em seguida, expanda o **fluxo de trabalho do SharePoint** nó.  
  
10. No **fluxo de trabalho do SharePoint** nó do **caixa de ferramentas**, execute um dos seguintes conjuntos de etapas:  
  
    -   Abra o menu de atalho para o **OnWorkflowItemChanged** atividade e, em seguida, escolha **cópia**. No designer de fluxo de trabalho, abra o menu de atalho para a linha dentro de **whileActivity1** atividade e, em seguida, escolha **colar**.  
  
    -   Arrastar o **OnWorkflowItemChanged** atividade do **caixa de ferramentas** para o designer de fluxo de trabalho e conecte-se a atividade para a linha dentro de **whileActivity1** atividade.  
  
11. Escolha o **onWorkflowItemChanged1** atividade.  
  
12. No **propriedades** janela, defina as propriedades conforme mostrado na tabela a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**CorrelationToken**|**workflowToken**|  
    |**Invocado**|**onWorkflowItemChanged**|  
  
## <a name="handle-activity-events"></a>Manipular eventos de atividade
 Por fim, verifique o status do documento de cada atividade. Se o documento foi revisado, o fluxo de trabalho é concluído.  
  
#### <a name="to-handle-activity-events"></a>Para manipular eventos de atividade  
  
1.  Na *Workflow1.cs* ou *Workflow1.vb*, adicione o seguinte campo na parte superior do `Workflow1` classe. Esse campo é usado em uma atividade para determinar se o fluxo de trabalho é concluído.  
  
    ```vb  
    Dim workflowPending As Boolean = True  
    ```  
  
    ```csharp  
    Boolean workflowPending = true;  
    ```  
  
2.  Adicione o seguinte método à classe `Workflow1`. Esse método verifica o valor da `Document Status` propriedade da lista de documentos para determinar se o documento foi revisado. Se o `Document Status` estiver definida como `Review Complete`, o `checkStatus` método define o `workflowPending` campo **false** para indicar que o fluxo de trabalho está pronto para concluir.  
  
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
  
3.  Adicione o seguinte código para o `onWorkflowActivated` e `onWorkflowItemChanged` métodos para chamar o `checkStatus` método. Quando o fluxo de trabalho é iniciado, o `onWorkflowActivated` chamadas de método a `checkStatus` método para determinar se o documento já foi revisado. Se não tiver sido revisado, o fluxo de trabalho continua. Quando o documento é salvo, o `onWorkflowItemChanged` chamadas de método a `checkStatus` método novamente para determinar se o documento foi revisado. Enquanto o `workflowPending` campo é definido como **verdadeiro**, o fluxo de trabalho continua a ser executado.  
  
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
  
4.  Adicione o seguinte código para o `isWorkflowPending` método para verificar o status do `workflowPending` propriedade. Cada vez que o documento é salvo, o **whileActivity1** atividade chama o `isWorkflowPending` método. Este método examina os <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> propriedade do <xref:System.Workflow.Activities.ConditionalEventArgs> objeto para determinar se o **WhileActivity1** atividade deve continuar ou concluir. Se a propriedade é definida como **verdadeira**, a atividade continua. Caso contrário, a atividade é concluída e o fluxo de trabalho for concluído.  
  
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
  
5.  Salvar o projeto.  
  
## <a name="test-the-sharepoint-workflow-template"></a>Teste o modelo de fluxo de trabalho do SharePoint
 Quando você inicia o depurador [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] implanta o modelo de fluxo de trabalho para o servidor do SharePoint e associa o fluxo de trabalho com o **documentos compartilhados** lista. Para testar o fluxo de trabalho, iniciar uma instância do fluxo de trabalho de um documento na **documentos compartilhados** lista.  
  
#### <a name="to-test-the-sharepoint-workflow-template"></a>Para testar o modelo de fluxo de trabalho do SharePoint  
  
1.  Na *Workflow1.cs* ou *Workflow1.vb*, defina um ponto de interrupção ao lado de **onWorkflowActivated** método.  
  
2.  Escolha o **F5** tecla para compilar e executar a solução.  
  
     O site do SharePoint é exibida.  
  
3.  No painel de navegação no SharePoint, escolha o **documentos compartilhados** link.  
  
4.  No **documentos compartilhados** , escolha o **documentos** no link a **ferramentas de biblioteca** guia e, em seguida, escolha o **carregar documento** botão .  
  
5.  No **carregar documento** caixa de diálogo, escolha o **procurar** botão, escolha qualquer arquivo de documento, escolha o **abrir** botão e, em seguida, escolha o **Okey** botão.  
  
     Isso carrega o documento selecionado para o **documentos compartilhados** listar e inicia o fluxo de trabalho.  
  
6.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], verifique se que o depurador é interrompido no ponto de interrupção ao lado de `onWorkflowActivated` método.  
  
7.  Escolha o **F5** tecla para continuar a execução.  
  
8.  Você pode alterar as configurações para o documento aqui, mas deixá-los com os valores padrão por enquanto, escolhendo a **salvar** botão.  
  
     Esse procedimento retornará o **documentos compartilhados** página do site da Web do SharePoint padrão.  
  
9. No **documentos compartilhados** página, verifique o valor abaixo de **MySharePointWorkflow - Workflow1** coluna estiver definida como **em andamento**. Isso indica que o fluxo de trabalho está em andamento e que o documento está aguardando revisão.  
  
10. No **documentos compartilhados** página, escolha o documento, escolha a seta que aparece e, em seguida, escolha o **editar propriedades** item de menu.  
  
11. Definir **Status do documento** à **Review Complete**e, em seguida, escolha o **salvar** botão.  
  
     Esse procedimento retornará o **documentos compartilhados** página do site da Web do SharePoint padrão.  
  
12. No **documentos compartilhados** página, verifique o valor abaixo de **Document Status** coluna estiver definida como **Review Complete**. Atualizar o **documentos compartilhados** página e verifique o valor abaixo de **MySharePointWorkflow - Workflow1** coluna estiver definida como **concluído**. Isso indica que fluxo de trabalho é concluído e que o documento foi revisado.  
  
## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar modelos de fluxo de trabalho a partir destes tópicos:  
  
-   Para saber mais sobre as atividades de fluxo de trabalho do SharePoint, consulte [atividades de fluxo de trabalho para o SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=178992).  
  
-   Para saber mais sobre as atividades do Windows Workflow Foundation, consulte [Activities Namespace](http://go.microsoft.com/fwlink/?LinkId=178993).  
  
## <a name="see-also"></a>Consulte também
 [Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)   
 [Projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md)   
 [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)  
  
