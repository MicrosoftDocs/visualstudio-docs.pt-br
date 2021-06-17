---
title: Depurar aplicativo do SharePoint usando o IntelliTrace
description: Use o IntelliTrace para depurar e corrigir aplicativos do SharePoint com mais facilidade. Criar e adicionar código a um receptor de recurso. Teste o projeto. Coletar dados do IntelliTrace.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cf7fa6c7255e05c465d6c209db5e9581a49aee64
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112841"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>Passo a passo: depurar um aplicativo do SharePoint usando o IntelliTrace

Usando o IntelliTrace, você pode depurar soluções do SharePoint com mais facilidade. Os depurador tradicionais lhe dão apenas um instantâneo de uma solução no momento atual. No entanto, você pode usar o IntelliTrace para revisar eventos passados que ocorreram em sua solução e o contexto no qual eles ocorreram e navegar até o código.

 Este passo a passo demonstra como depurar um projeto do SharePoint no Visual Studio usando o Microsoft Monitoring Agent para coletar dados do IntelliTrace de aplicativos implantados. Para analisar esses dados, você deve usar Visual Studio Enterprise. Este projeto incorpora um receptor de recursos que, quando o recurso é ativado, adiciona uma tarefa à lista Tarefa e um comunicado à lista de Anúncios. Quando o recurso é desativado, a tarefa é marcada como concluída e um segundo comunicado é adicionado à lista de Anúncios. No entanto, o procedimento contém um erro lógico que impede que o projeto seja executado corretamente. Usando o IntelliTrace, você localizará e corrigirá o erro.

 **Aplica-se a:** As informações neste tópico se aplica às soluções do SharePoint que foram criadas no Visual Studio.

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

## <a name="create-a-feature-receiver"></a>Criar um receptor de recurso

Primeiro, você cria um projeto vazio do SharePoint que tem um receptor de recursos.

1. Crie um projeto de solução do SharePoint destinado à versão do SharePoint instalada e nomee-o **Como IntelliTraceTest.**

     O **Assistente de Personalização do SharePoint** é exibido, no qual você pode especificar o site do SharePoint para seu projeto e o nível de confiança da solução.

2. Escolha o **botão de opção Implantar como uma solução de farm** e, em seguida, escolha o **botão** Concluir.

     O IntelliTrace opera apenas em soluções de farm.

3. No **Gerenciador de Soluções**, abra o menu de atalho para o **nó Recursos** e escolha Adicionar **Recurso**.

     *Feature1.feature* é exibido.

4. Abra o menu de atalho para Feature1.feature e escolha Adicionar Receptor **de Eventos** para adicionar um módulo de código ao recurso.

## <a name="add-code-to-the-feature-receiver"></a>Adicionar código ao receptor do recurso

Em seguida, adicione código a dois métodos no receptor do recurso: `FeatureActivated` e `FeatureDeactivating` . Esses métodos são disparados sempre que um recurso é ativado ou desativado no SharePoint, respectivamente.

1. Na parte superior da classe, adicione o seguinte código, que declara variáveis que especificam o site e `Feature1EventReceiver` o subsite do SharePoint:

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

## <a name="test-the-project"></a>Testar o projeto

Agora que o código foi adicionado ao receptor do recurso e o coletor de dados está em execução, implante e execute a solução do SharePoint para testar se ele funciona corretamente.

> [!IMPORTANT]
> Neste exemplo, um erro é lançado no manipulador de eventos FeatureDeactivating. Mais adiante neste passo a passo, você localizará esse erro usando o arquivo .iTrace criado pelo coletor de dados.

1. Implante a solução no SharePoint e abra o site do SharePoint em um navegador.

     O recurso é ativado automaticamente, fazendo com que seu receptor de recursos adicione um comunicado e uma tarefa.

2. Exibir o conteúdo das listas Anúncios e Tarefas.

     A lista Anúncios deve ter um novo comunicado chamado recurso **ativado: IntelliTraceTest_Feature1** e a lista Tarefas deve ter uma nova tarefa chamada Desativar **recurso: IntelliTraceTest_Feature1**. Se um desses itens estiver ausente, verifique se o recurso está ativado. Se ele não estiver ativado, ative-o.

3. Desative o recurso executando as seguintes etapas:

   1. No menu **Ações do Site** no SharePoint, escolha **Configurações do Site**.

   2. Em **Ações do Site**, escolha o link Gerenciar recursos **do** site.

   3. Ao lado **de IntelliTraceTest Feature1**, escolha **o botão Desativar.**

   4. Na página Aviso, escolha o link **Desativar esse recurso.**

      O manipulador de eventos FeatureDeactivating() lança um erro.

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>Coletar dados do IntelliTrace usando Microsoft Monitoring Agent

Se você instalar Microsoft Monitoring Agent no sistema que está executando o SharePoint, poderá depurar soluções do SharePoint usando dados mais específicos do que as informações genéricas retornadas pelo IntelliTrace. O agente funciona fora do Visual Studio usando cmdlets do PowerShell para capturar informações de depuração enquanto sua solução do SharePoint é executado.

> [!NOTE]
> As informações de configuração nesta seção são específicas para este exemplo. Para obter mais informações sobre outras opções de configuração, [consulte Usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).

1. No computador que está executando o SharePoint, [configurar o Microsoft Monitoring Agent e começar a monitorar sua solução.](../debugger/using-the-intellitrace-stand-alone-collector.md)

2. Desative o recurso:

   1. No menu **Ações do Site** no SharePoint, escolha **Configurações do Site**.

   2. Em **Ações do Site**, escolha o link Gerenciar recursos **do** site.

   3. Ao lado **de IntelliTraceTest Feature1**, escolha **o botão Desativar.**

   4. Na página Aviso, escolha o link **Desativar esse recurso.**

      Ocorre um erro (nesse caso, devido ao erro lançado no manipulador de eventos FeatureDeactivating()).

3. Na janela do PowerShell, execute o comando [Stop-WebApplicationMonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20)) para criar o arquivo .iTrace, interromper o monitoramento e reiniciar sua solução do SharePoint.

     **Stop-WebApplicationMonitoring***"<\<SharePointSite> \\ SharePointAppName \> "*  

## <a name="debug-and-fix-the-sharepoint-solution"></a>Depurar e corrigir a solução do SharePoint

Agora você pode exibir o arquivo de log do IntelliTrace Visual Studio para encontrar e corrigir o erro na solução do SharePoint.

1. Na pasta \IntelliTraceLogs, abra o arquivo .iTrace no Visual Studio.

     A **página Resumo do IntelliTrace** é exibida. Como o erro não foi tratado, uma ID de correlação do SharePoint (um GUID) aparece na área de exceção sem manipulação da **seção** Análise. Escolha o **botão Pilha de** Chamada se quiser exibir a pilha de chamada em que o erro ocorreu.

2. Escolha o **botão Depurar Exceção.**

     Se solicitado, carregue arquivos de símbolo. Na janela **do IntelliTrace,** a exceção é realçada como "Lançada: Erro grave!".

     Na janela do IntelliTrace, escolha a exceção para exibir o código que falhou.

3. Corrige o erro abrindo a solução do SharePoint e, em seguida, comentando ou removendo a instrução **throw** na parte superior do procedimento FeatureDeactivating().

4. Reimplante a solução Visual Studio e, em seguida, reimplante-a no SharePoint.

5. Desative o recurso executando as seguintes etapas:

    1. No menu **Ações do Site** no SharePoint, escolha **Configurações do Site**.

    2. Em **Ações do Site**, escolha o link Gerenciar recursos **do** site.

    3. Ao lado **de IntelliTraceTest Feature1**, escolha **o botão Desativar.**

    4. Na página Aviso, escolha o link **Desativar esse recurso.**

6. Abra a lista Tarefa e verifique se o **valor status** da tarefa Desativar é "Concluído" e seu **valor %** Concluído é 100%.

     O código agora é executado corretamente.

## <a name="see-also"></a>Confira também

- [Verificar e depurar o código do SharePoint](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [Passo a passo: verificar o código do SharePoint usando testes de unidade](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))
