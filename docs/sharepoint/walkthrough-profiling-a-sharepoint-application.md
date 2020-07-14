---
title: 'Walkthrough: criando perfil de um aplicativo do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c900a1496d3ef864e50d40092379348c05a4706b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017105"
---
# <a name="walkthrough-profile-a-sharepoint-application"></a>Walkthrough: criar perfil de um aplicativo do SharePoint
  Este tutorial mostra como usar as ferramentas de criação de perfil no Visual Studio para otimizar o desempenho de um aplicativo do SharePoint. O aplicativo de exemplo é um receptor de evento de recurso do SharePoint que contém um loop ocioso que degrada o desempenho do receptor de evento de recurso. O criador de perfil do Visual Studio permite que você localize e elimine a parte mais cara (com desempenho mais lento) do projeto, também conhecida como o *caminho quente*.

 Este tutorial demonstra as seguintes tarefas:

- [Adicione um receptor de evento de recurso e recurso](#add-a-feature-and-feature-event-receiver).

- [Configure e implante o aplicativo do SharePoint](#configure-and-deploy-the-sharepoint-application).

- [Execute o aplicativo do SharePoint](#run-the-sharepoint-application).

- [Exibir e interpretar os resultados do perfil](#view-and-interpret-the-profile-results).

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Microsoft Windows e do SharePoint.

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-sharepoint-project"></a>Criar um projeto do SharePoint
 Primeiro, crie um projeto do SharePoint.

### <a name="to-create-a-sharepoint-project"></a>Para criar um projeto do SharePoint

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. No painel modelos, escolha o modelo de **projeto do SharePoint 2010** .

4. Na caixa **nome** , digite **ProfileTest**e, em seguida, escolha o botão **OK** .

    O **Assistente para personalização do SharePoint** é exibido.

5. Na página **especificar o site e o nível de segurança para depuração** , insira a URL para o site do SharePoint Server em que você deseja depurar a definição do site ou use o local padrão (<em>nome do sistema</em>http:///).

6. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** .

    No momento, você só pode criar o perfil de soluções de farm. Para obter mais informações sobre soluções em área restrita versus soluções de farm, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7. Escolha o botão **Concluir**. O projeto aparece no **Gerenciador de soluções**.

## <a name="add-a-feature-and-feature-event-receiver"></a>Adicionar um receptor de evento de recurso e recurso
 Em seguida, adicione um recurso ao projeto junto com um receptor de evento para o recurso. Esse receptor de evento conterá o código a ser criado para o perfil.

### <a name="to-add-a-feature-and-feature-event-receiver"></a>Para adicionar um receptor de eventos de recurso e recurso

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó **recursos** , escolha **Adicionar recurso**e deixe o nome no valor padrão, **Feature1**.

2. No **Gerenciador de soluções**, abra o menu de atalho para **Feature1**e escolha **Adicionar receptor de eventos**.

     Isso adiciona um arquivo de código ao recurso com vários manipuladores de eventos comentados e abre o arquivo para edição.

3. Na classe receptor de evento, adicione as seguintes declarações de variável.

    ```vb
    ' SharePoint site/subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site/subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

4. Substitua o `FeatureActivated` procedimento pelo código a seguir.

    ```vb
    Public Overrides Sub FeatureActivated(properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add a new announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    ' Waste some time.
                    TimeCounter()
                    ' Update the list.
                    listItem.Update()
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

                    // Add a new announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " +
    DateTime.Now.ToString();
                    // Waste some time.
                    TimeCounter();
                    // Update the list.
                    listItem.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

5. Adicione o procedimento a seguir abaixo do `FeatureActivated` procedimento.

    ```vb

    Public Sub TimeCounter()
        Dim result As Integer
        For i As Integer = 0 To 99999
            For j As Integer = 0 To 9999
                result = i * j
            Next j
        Next i
    End Sub
    ```

    ```csharp
    public void TimeCounter()
    {
        for (int i = 0; i < 100000; i++)
        {
            for (int j = 0; j < 10000; j++)
            {
                int result = i * j;
            }
        }
    }
    ```

6. No **Gerenciador de soluções**, abra o menu de atalho do projeto (**ProfileTest**) e escolha **Propriedades**.

7. Na caixa de diálogo **Propriedades** , escolha a guia **SharePoint** .

8. Na lista **configuração de implantação ativa** , escolha **sem ativação**.

     A seleção dessa configuração de implantação permite que você ative manualmente o recurso mais tarde no SharePoint.

9. Salve o projeto.

## <a name="configure-and-deploy-the-sharepoint-application"></a>Configurar e implantar o aplicativo do SharePoint
 Agora que o projeto do SharePoint está pronto, configure-o e implante-o no servidor do SharePoint.

### <a name="to-configure-and-deploy-the-sharepoint-application"></a>Para configurar e implantar o aplicativo do SharePoint

1. No menu **analisar** , escolha **Iniciar assistente de desempenho**.

2. Na página um do **Assistente de desempenho**, deixe o método de criação de perfil como **amostragem de CPU** e escolha o botão **Avançar** .

     Os outros métodos de criação de perfil podem ser usados em situações de criação de perfil mais avançadas. Para obter mais informações, consulte [Noções Básicas sobre Métodos de Coleta de Desempenho](../profiling/understanding-performance-collection-methods.md).

3. Na página dois do **Assistente de desempenho**, deixe o destino do perfil como **ProfileTest** e escolha o botão **Avançar** .

     Se uma solução tiver vários projetos, eles aparecerão nessa lista.

4. Na página três do **Assistente de desempenho**, desmarque a caixa de seleção **Habilitar criação de perfil de interação de camada** e, em seguida, escolha o botão **Avançar** .

     O recurso TIP (criação de perfil de interação de camada) é útil para medir o desempenho de aplicativos que consultam bancos de dados e mostrar o número de vezes que uma página da Web é solicitada. Como esses dados não são necessários para este exemplo, não Habilitaremos esse recurso.

5. Na página quatro do **Assistente de desempenho**, deixe a caixa de seleção **Iniciar criação de perfil após o assistente ser concluído** e escolha o botão **concluir** .

     O assistente habilita a criação de perfil de aplicativo no servidor, exibe a janela de **Gerenciador de desempenho** e, em seguida, compila, implanta e executa o aplicativo do SharePoint.

## <a name="run-the-sharepoint-application"></a>Executar o aplicativo do SharePoint
 Ative o recurso no SharePoint, disparando o `FeatureActivation` código do evento a ser executado.

### <a name="to-run-the-sharepoint-application"></a>Para executar o aplicativo do SharePoint

1. No SharePoint, abra o menu **ações do site** e, em seguida, escolha configurações do **site**.

2. Na lista **ações do site** , escolha o link **gerenciar recursos do site** .

3. Na lista de **recursos** , escolha o botão **Ativar** ao lado de **ProfileTest Feature1**.

     Há uma pausa quando você faz isso, devido ao loop ocioso sendo chamado na `FeatureActivated` função.

4. Na barra **início rápido** , escolha **listas** e, em seguida, na lista **listas** , escolha **anúncios**.

     Observe que um novo comunicado foi adicionado à lista informando que o recurso foi ativado.

5. Feche o site do SharePoint.

     Depois de fechar o SharePoint, o criador de perfil cria e exibe um exemplo de relatório de criação de perfil e o salva como um arquivo. vsp na pasta do projeto **ProfileTest** .

## <a name="view-and-interpret-the-profile-results"></a>Exibir e interpretar os resultados do perfil
 Agora que você executou e criou o perfil do aplicativo do SharePoint, exiba os resultados do teste.

### <a name="to-view-and-interpret-the-profile-results"></a>Para exibir e interpretar os resultados do perfil

1. Na seção **funções fazendo o mais individual** do relatório de criação de perfil de exemplo, observe que `TimeCounter` está próximo à parte superior da lista.

     Esse local indica que `TimeCounter` foi uma das funções com o maior número de amostras, o que significa que se trata de um dos maiores afunilamentos de desempenho no aplicativo. No entanto, essa situação não é surpreendente porque foi projetada de forma intencional para fins de demonstração.

2. Na seção **funções fazendo o trabalho mais individual** , escolha o `ProcessRequest` link para exibir a distribuição de custo para a `ProcessRequest` função.

     Na seção **funções chamadas** para `ProcessRequest` , observe que a função **FeatureActiviated** está listada como a função chamada mais cara.

3. Na seção **funções chamadas** , escolha o botão **FeatureActivated** .

     Na seção **funções chamadas** para **FeatureActivated**, a `TimeCounter` função é listada como a função chamada mais cara. No painel **exibição de código de função** , o código realçado ( `TimeCounter` ) é o HotSpot e indica onde a correção é necessária.

4. Feche o relatório de criação de perfil de exemplo.

     Para exibir o relatório novamente a qualquer momento, abra o arquivo. vsp na janela **Gerenciador de desempenho** .

## <a name="fix-the-code-and-reprofile-the-application"></a>Corrigir o código e recriar o perfil do aplicativo
 Agora que a função de HotSpot no aplicativo do SharePoint foi identificada, corrija-a.

### <a name="to-fix-the-code-and-reprofile-the-application"></a>Para corrigir o código e recriar o perfil do aplicativo

1. No código do receptor de evento de recurso, comente a `TimeCounter` chamada de método no `FeatureActivated` para impedir que ela seja chamada.

2. Salve o projeto.

3. No **Gerenciador de desempenho**, abra a pasta destinos e escolha o nó **ProfileTest** .

4. Na barra de ferramentas **Gerenciador de desempenho** , na guia **ações** , escolha o botão **Iniciar criação de perfil** .

     Se você quiser alterar qualquer uma das propriedades de criação de perfil antes de reprofiling o aplicativo, escolha o botão **Assistente de inicialização de desempenho** em vez disso.

5. Siga as instruções na seção **executando o aplicativo do SharePoint** , anteriormente neste tópico.

     O recurso deve ser ativado muito mais rapidamente agora que a chamada para o loop ocioso foi eliminada. O relatório de criação de perfil de exemplo deve refletir isso.

## <a name="see-also"></a>Consulte também
- [Visão geral da sessão de desempenho](../profiling/performance-session-overview.md)
- [Guia do iniciante à criação de perfil do desempenho](../profiling/beginners-guide-to-performance-profiling.md)
- [Encontrar afunilamentos de aplicativos com o Visual Studio Profiler](https://msdn.microsoft.com/magazine/cc337887.aspx)
