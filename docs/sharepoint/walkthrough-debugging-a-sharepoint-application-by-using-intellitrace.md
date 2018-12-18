---
title: 'Passo a passo: Depurando um aplicativo do SharePoint usando o IntelliTrace | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IntelliTrace [SharePoint development in Visual Studio]
- standalone data collector
- SharePoint development in Visual Studio, IntelliTrace
- data collector
- IntelliTrace
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 59f801c79c8bb19a63064bdac2fe717ee3e3a845
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295573"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>Passo a passo: Depurar um aplicativo do SharePoint usando o IntelliTrace

Usando o IntelliTrace, você pode depurar mais facilmente soluções do SharePoint. Depuradores tradicionais fornecem apenas um instantâneo de uma solução no momento atual. No entanto, você pode usar o IntelliTrace para examinar os últimos eventos que ocorreram na sua solução e o contexto em que ocorreu e navegue até o código.

 Este passo a passo demonstra como depurar um projeto do SharePoint 2010 ou SharePoint 2013 no Visual Studio usando o Microsoft Monitoring Agent para coletar dados do IntelliTrace de aplicativos implantados. Para analisar os dados, você deve usar o Visual Studio Enterprise. Este projeto incorpora um receptor de recurso que, quando o recurso é ativado, adiciona uma tarefa à lista de tarefas e um comunicado para a lista de avisos. Quando o recurso for desativado, a tarefa é marcada como concluída e um segundo aviso é adicionado à lista de anúncios. No entanto, o procedimento contém um erro de lógico que impede que o projeto sendo executado corretamente. Usando o IntelliTrace, você localizar e corrigir o erro.

 **Aplica-se a:** as informações neste tópico se aplicam às soluções do SharePoint 2010 e SharePoint 2013 que foram criadas no Visual Studio.

 Esta explicação passo a passo ilustra as seguintes tarefas:

- [Criar um receptor de recurso](#BKMK_CreateReceiver)

- [Adicione código ao receptor do recurso](#BKMK_AddCode)

- [O projeto de teste](#BKMK_Test1)

- [Coletar dados do IntelliTrace usando o Microsoft Monitoring Agent](#BKMK_CollectDiagnosticData)

- [Depurar e corrigir a solução do SharePoint](#BKMK_DebugSolution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

- Edições com suporte do Windows e do SharePoint.

- Visual Studio Enterprise.

## <a name="create-a-feature-receiver"></a>Criar um receptor de recurso

Primeiro, crie um projeto vazio do SharePoint que tem um receptor de recurso.

1. Crie um projeto de solução do SharePoint 2010 ou SharePoint 2013 e nomeie- **IntelliTraceTest**.

     O **Assistente para personalização do SharePoint** for exibida, na qual você pode especificar o site do SharePoint para seu projeto e o nível de confiança da solução.

2. Escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão.

     IntelliTrace funciona somente em soluções de farm.

3. Na **Gerenciador de soluções**, abra o menu de atalho para o **recursos** nó e, em seguida, escolha **adicionar recurso**.

     *Feature1.Feature* é exibida.

4. Abra o menu de atalho para Feature1.feature e, em seguida, escolha **adicionar receptor de evento** para adicionar um módulo de código para o recurso.

## <a name="add-code-to-the-feature-receiver"></a>Adicione código ao receptor do recurso

Em seguida, adicione código para dois métodos no receptor do recurso: `FeatureActivated` e `FeatureDeactivating`. Esses métodos disparam sempre que um recurso é ativado ou desativado no SharePoint, respectivamente.

1. Na parte superior do `Feature1EventReceiver` de classe, adicione o código a seguir, que declara variáveis que especificam o site do SharePoint e o subsite:

    ```vb
    ' SharePoint site and subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site and subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

2. Substitua o método `FeatureActivated` pelo seguinte código:

    ```vb
    Public Overrides Sub FeatureActivated(ByVal properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")
                    Dim taskList As SPList = web.Lists("Tasks")

                    ' Add an announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Add a task to the Task list.
                    Dim newTask As SPListItem = taskList.Items.Add()
                    newTask("Title") = "Deactivate feature: " & Convert.ToString(properties.Definition.DisplayName)
                    newTask.Update()
                End Using
            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureActivated(SPFeatureReceiverProperties properties)
    {
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList announcementsList = web.Lists["Announcements"];
                    SPList taskList = web.Lists["Tasks"];

                    // Add an announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Add a task to the Task list.
                    SPListItem newTask = taskList.Items.Add();
                    newTask["Title"] = "Deactivate feature: " + properties.Definition.DisplayName;
                    newTask.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }

    }
    ```

3. Substitua o método `FeatureDeactivating` pelo seguinte código:

    ```vb
    Public Overrides Sub FeatureDeactivating(ByVal properties As SPFeatureReceiverProperties)
        ' The following line induces an error to demonstrate debugging.
        ' Remove this line later for proper operation.
        Throw New System.InvalidOperationException("Serious error occurred!")
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim taskList As SPList = web.Lists("Tasks")
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add an announcement that the feature was deactivated.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Deactivated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was deactivated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Find the task that the feature receiver added to the Task list when the
                    ' feature was activated.
                    Dim qry As New SPQuery()
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>"
                    Dim taskItems As SPListItemCollection = taskList.GetItems(qry)

                    For Each taskItem As SPListItem In taskItems
                        ' Mark the task as complete.
                        taskItem("PercentComplete") = 1
                        taskItem("Status") = "Completed"
                        taskItem.Update()
                    Next
                End Using

            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
    {
        // The following line induces an error to demonstrate debugging.
        // Remove this line later for proper operation.
        throw new System.InvalidOperationException("A serious error occurred!"); 
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList taskList = web.Lists["Tasks"];
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add an announcement that the feature was deactivated.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Deactivated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was deactivated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Find the task that the feature receiver added to the Task list when the
                    // feature was activated.
                    SPQuery qry = new SPQuery();
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>";
                    SPListItemCollection taskItems = taskList.GetItems(qry);

                    foreach (SPListItem taskItem in taskItems)
                    {
                        // Mark the task as complete.
                        taskItem["PercentComplete"] = 1;
                        taskItem["Status"] = "Completed";
                        taskItem.Update();
                    }
                }
            }

        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

## <a name="test-the-project"></a>O projeto de teste

Agora que o código é adicionado ao receptor do recurso e o coletor de dados está em execução, implante e execute a solução do SharePoint para testar se ele funciona corretamente.

> [!IMPORTANT]
> Neste exemplo, um erro será lançado no manipulador de eventos FeatureDeactivating. Posteriormente neste passo a passo, você pode localizar esse erro usando o arquivo. itrace que criou o coletor de dados.

1. Implantar a solução do SharePoint e, em seguida, abra o site do SharePoint em um navegador.

     O recurso ativa automaticamente, fazendo com que seu receptor de recurso Adicionar um comunicado e uma tarefa.

2. Exiba o conteúdo das listas de tarefas e anúncios.

     A lista de avisos deve ter um novo comunicado é denominado **recurso ativado: IntelliTraceTest_Feature1**, e a lista de tarefas deve ter uma nova tarefa que é denominada **Desativar recurso: IntelliTraceTest_ Feature1**. Se nenhum desses itens estiver ausente, verifique se o recurso é ativado. Se não estiver ativado, ativá-lo.

3. Desative o recurso, executando as seguintes etapas:

   1. Sobre o **ações do Site** menu no SharePoint, escolha **configurações de Site**.

   2. Sob **ações do Site**, escolha o **gerenciar recursos do site** link.

   3. Lado **IntelliTraceTest Feature1**, escolha o **desativar** botão.

   4. Na página de aviso, escolha o **desativar esse recurso** link.

      O manipulador de eventos FeatureDeactivating() gera um erro.

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>Coletar dados do IntelliTrace usando o Microsoft Monitoring Agent

Se você instalar o Microsoft Monitoring Agent no sistema que está executando o SharePoint, você pode depurar soluções do SharePoint por meio de dados que é mais específicos do que as informações genéricas que retorna do IntelliTrace. O agente funciona fora do Visual Studio usando cmdlets do PowerShell para capturar informações de depuração durante as execuções de solução do SharePoint.

> [!NOTE]
> As informações de configuração nesta seção são específicas para este exemplo. Para obter mais informações sobre outras opções de configuração, consulte [usando o coletor autônomo IntelliTrace](/visualstudio/debugger/using-the-intellitrace-stand-alone-collector).

1. No computador que está executando o SharePoint, [configurar o Microsoft Monitoring Agent e começar a monitorar sua solução](/visualstudio/debugger/using-the-intellitrace-stand-alone-collector).

2. Desative o recurso:

   1. Sobre o **ações do Site** menu no SharePoint, escolha **configurações de Site**.

   2. Sob **ações do Site**, escolha o **gerenciar recursos do site** link.

   3. Lado **IntelliTraceTest Feature1**, escolha o **desativar** botão.

   4. Na página de aviso, escolha o **desativar esse recurso** link.

      Ocorrerá um erro (nesse caso, devido ao erro lançado no manipulador de eventos FeatureDeactivating()).

3. Na janela do PowerShell, execute as [Stop-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313687) comando para criar o arquivo. itrace, parar de monitorar e reiniciar sua solução do SharePoint.

     **Stop-WebApplicationMonitoring**  *"\<SharePointSite>\\<SharePointAppName\>"*

## <a name="debug-and-fix-the-sharepoint-solution"></a>Depurar e corrigir a solução do SharePoint

Agora você pode exibir o arquivo de log do IntelliTrace no Visual Studio para encontrar e corrigir o erro na solução do SharePoint.

1. Na pasta \IntelliTraceLogs, abra o arquivo. itrace no Visual Studio.

     O **resumo do IntelliTrace** página será exibida. Porque o erro não foi tratado, uma ID de correlação do SharePoint (um GUID) aparece na área de exceção sem tratamento do **análise** seção. Escolha o **pilha de chamadas** botão se você quiser exibir a pilha de chamadas onde ocorreu o erro.

2. Escolha o **exceção da depuração** botão.

     Se solicitado, carrega arquivos de símbolo. No **IntelliTrace** janela, a exceção é realçada como "lançada: erro grave!".

     Na janela IntelliTrace, escolha a exceção para exibir o código que falhou.

3. Corrigir o erro ao abrir a solução do SharePoint e, em seguida, comentar ou remover as **lançar** instrução na parte superior do procedimento FeatureDeactivating().

4. Recompile a solução no Visual Studio e, em seguida, reimplantá-lo no SharePoint.

5. Desative o recurso, executando as seguintes etapas:

    1. Sobre o **ações do Site** menu no SharePoint, escolha **configurações de Site**.

    2. Sob **ações do Site**, escolha o **gerenciar recursos do site** link.

    3. Lado **IntelliTraceTest Feature1**, escolha o **desativar** botão.

    4. Na página de aviso, escolha o **desativar esse recurso** link.

6. Abra a lista de tarefas e verifique se que o **Status** o valor da tarefa Deactivate for "concluído" e seu **% concluída** valor é 100%.

     O código agora é executado corretamente.

## <a name="see-also"></a>Consulte também

[Verificar e depurar o código do SharePoint](../sharepoint/verifying-and-debugging-sharepoint-code.md)  
[IntelliTrace](/visualstudio/debugger/intellitrace)  
[Passo a passo: Verifique se o código do SharePoint usando testes de unidade](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))
