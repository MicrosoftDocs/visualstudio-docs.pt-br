---
title: Depurar aplicativo do SharePoint usando o IntelliTrace
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IntelliTrace [SharePoint development in Visual Studio]
- standalone data collector
- SharePoint development in Visual Studio, IntelliTrace
- data collector
- IntelliTrace
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 041a110ee39ae7711756b8d689bdf68ae2368caf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015757"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>Walkthrough: Depurar um aplicativo do SharePoint usando o IntelliTrace

Usando o IntelliTrace, você pode depurar soluções do SharePoint com mais facilidade. Os depuradores tradicionais oferecem apenas um instantâneo de uma solução no momento atual. No entanto, você pode usar o IntelliTrace para examinar eventos passados que ocorreram em sua solução e o contexto no qual eles ocorreram e navegar até o código.

 Este tutorial demonstra como depurar um projeto do SharePoint 2010 ou do SharePoint 2013 no Visual Studio usando Microsoft Monitoring Agent para coletar dados do IntelliTrace de aplicativos implantados. Para analisar esses dados, você deve usar Visual Studio Enterprise. Este projeto incorpora um receptor de recursos que, quando o recurso é ativado, adiciona uma tarefa à lista de tarefas e um comunicado à lista de anúncios. Quando o recurso é desativado, a tarefa é marcada como concluída e um segundo comunicado é adicionado à lista comunicados. No entanto, o procedimento contém um erro lógico que impede que o projeto seja executado corretamente. Usando o IntelliTrace, você localizará e corrigirá o erro.

 **Aplica-se a:** As informações neste tópico se aplicam às soluções do SharePoint 2010 e do SharePoint 2013 que foram criadas no Visual Studio.

 Este passo a passo ilustra as seguintes tarefas:

- [Criar um Receptor do Recurso](#create-a-feature-receiver)

- [Adicionar Código ao Receptor do Recurso](#add-code-to-the-feature-receiver)

- [Testar o projeto](#test-the-project)

- [Coletar dados do IntelliTrace usando Microsoft Monitoring Agent](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [Depurar e Corrigir a Solução do SharePoint](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Windows e do SharePoint.

- Visual Studio Enterprise.

## <a name="create-a-feature-receiver"></a>Criar um receptor de recursos

Primeiro, você cria um projeto do SharePoint vazio que tem um receptor de recursos.

1. Crie um projeto de solução do SharePoint 2010 ou SharePoint 2013 e nomeie-o **intellitracetest**.

     O **Assistente para personalização do SharePoint** é exibido, no qual você pode especificar o site do SharePoint para o seu projeto e o nível de confiança da solução.

2. Escolha o botão de opção **implantar como uma solução de farm** e, em seguida, escolha o botão **concluir** .

     O IntelliTrace funciona apenas em soluções de farm.

3. No **Gerenciador de soluções**, abra o menu de atalho do nó **recursos** e escolha **Adicionar recurso**.

     *Feature1. Feature* é exibido.

4. Abra o menu de atalho para Feature1. Feature e escolha **Adicionar receptor de eventos** para adicionar um módulo de código ao recurso.

## <a name="add-code-to-the-feature-receiver"></a>Adicionar código ao receptor de recursos

Em seguida, adicione o código a dois métodos no receptor de recursos: `FeatureActivated` e `FeatureDeactivating` . Esses métodos são disparados sempre que um recurso é ativado ou desativado no SharePoint, respectivamente.

1. Na parte superior da `Feature1EventReceiver` classe, adicione o código a seguir, que declara variáveis que especificam o site e o subsite do SharePoint:

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

## <a name="test-the-project"></a>Teste do projeto

Agora que o código foi adicionado ao receptor de recursos e o coletor de dados está em execução, implante e execute a solução do SharePoint para testar se ele funciona corretamente.

> [!IMPORTANT]
> Para este exemplo, um erro é gerado no manipulador de eventos FeatureDeactivating. Mais adiante neste tutorial, você Localizará esse erro usando o arquivo. iTrace que o coletor de dados criou.

1. Implante a solução no SharePoint e, em seguida, abra o site do SharePoint em um navegador.

     O recurso é ativado automaticamente, fazendo com que seu receptor de recursos adicione um anúncio e uma tarefa.

2. Exibir o conteúdo das listas de anúncios e tarefas.

     A lista de comunicados deve ter um novo comunicado chamado **recurso ativado: IntelliTraceTest_Feature1**e a lista de tarefas deve ter uma nova tarefa denominada **recurso desativar: IntelliTraceTest_Feature1**. Se um desses itens estiver ausente, verifique se o recurso está ativado. Se não estiver ativado, ative-o.

3. Desative o recurso executando as seguintes etapas:

   1. No menu **ações do site** no SharePoint, escolha **configurações do site**.

   2. Em **ações do site**, escolha o link **gerenciar recursos do site** .

   3. Ao lado de **intellitracetest Feature1**, escolha o botão **desativar** .

   4. Na página de aviso, escolha o link **desativar este recurso** .

      O manipulador de eventos FeatureDeactivating () gera um erro.

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>Coletar dados do IntelliTrace usando Microsoft Monitoring Agent

Se você instalar Microsoft Monitoring Agent no sistema que está executando o SharePoint, poderá depurar soluções do SharePoint usando dados mais específicos do que as informações genéricas que o IntelliTrace retorna. O agente funciona fora do Visual Studio usando cmdlets do PowerShell para capturar informações de depuração enquanto sua solução do SharePoint é executada.

> [!NOTE]
> As informações de configuração nesta seção são específicas para este exemplo. Para obter mais informações sobre outras opções de configuração, consulte [usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).

1. No computador que está executando o SharePoint, [configure Microsoft Monitoring Agent e comece a monitorar sua solução](../debugger/using-the-intellitrace-stand-alone-collector.md).

2. Desativar o recurso:

   1. No menu **ações do site** no SharePoint, escolha **configurações do site**.

   2. Em **ações do site**, escolha o link **gerenciar recursos do site** .

   3. Ao lado de **intellitracetest Feature1**, escolha o botão **desativar** .

   4. Na página de aviso, escolha o link **desativar este recurso** .

      Ocorre um erro (nesse caso, devido ao erro gerado no manipulador de eventos FeatureDeactivating ()).

3. Na janela do PowerShell, execute o comando [Stop-WebApplicationMonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20)) para criar o arquivo. itrace, parar o monitoramento e reiniciar a solução do SharePoint.

     **Stop-WebApplicationMonitoring***" \<SharePointSite> \\<SharePointAppName \> "*  

## <a name="debug-and-fix-the-sharepoint-solution"></a>Depurar e corrigir a solução do SharePoint

Agora você pode exibir o arquivo de log do IntelliTrace no Visual Studio para localizar e corrigir o erro na solução do SharePoint.

1. Na pasta \IntelliTraceLogs, abra o arquivo. iTrace no Visual Studio.

     A página **Resumo do IntelliTrace** é exibida. Como o erro não foi tratado, uma ID de correlação do SharePoint (um GUID) aparece na área de exceção sem tratamento da seção **análise** . Escolha o botão **pilha de chamadas** se desejar exibir a pilha de chamadas onde ocorreu o erro.

2. Escolha o botão **depurar exceção** .

     Se solicitado, carregue os arquivos de símbolo. Na janela do **IntelliTrace** , a exceção é realçada como "lançado: erro sério!".

     Na janela do IntelliTrace, escolha a exceção para exibir o código que falhou.

3. Corrija o erro abrindo a solução do SharePoint e, em seguida, comentando ou removendo a instrução **throw** na parte superior do procedimento FeatureDeactivating ().

4. Recompile a solução no Visual Studio e reimplante-a no SharePoint.

5. Desative o recurso executando as seguintes etapas:

    1. No menu **ações do site** no SharePoint, escolha **configurações do site**.

    2. Em **ações do site**, escolha o link **gerenciar recursos do site** .

    3. Ao lado de **intellitracetest Feature1**, escolha o botão **desativar** .

    4. Na página de aviso, escolha o link **desativar este recurso** .

6. Abra a lista de tarefas e verifique se o valor de **status** da tarefa de desativação está "concluído" e se seu valor de **% concluído** é 100%.

     O código agora é executado corretamente.

## <a name="see-also"></a>Consulte também

- [Verificar e depurar o código do SharePoint](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [Walkthrough: verificar o código do SharePoint usando testes de unidade](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))