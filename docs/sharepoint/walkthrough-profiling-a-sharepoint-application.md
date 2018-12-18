---
title: 'Passo a passo: Criação de perfil de um aplicativo do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5db5e9408a64df80311667267561ee69234fd7d5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852734"
---
# <a name="walkthrough-profile-a-sharepoint-application"></a>Passo a passo: Criar o perfil de um aplicativo do SharePoint
  Este passo a passo mostra como usar as ferramentas de criação de perfil no Visual Studio para otimizar o desempenho de um aplicativo do SharePoint. O aplicativo de exemplo é um receptor de evento de recurso do SharePoint que contém um loop ocioso que pode degradar o desempenho do receptor de evento do recurso. O criador de perfil do Visual Studio permite que você localize e eliminar a parte mais cara (desempenho mais lento) do projeto, também conhecido como o *afunilamento*.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- [Adicionando um recurso e o receptor de evento de recurso](#BKMK_AddFtrandFtrEvntReceiver).  
  
- [Configurando e implantando o aplicativo do SharePoint](#BKMK_ConfigSharePointApp).  
  
- [Executando o aplicativo do SharePoint](#BKMK_RunSPApp).  
  
- [Exibir e interpretar os resultados de criação de perfil](#BKMK_ViewResults).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do Microsoft Windows e do SharePoint.
  
-   [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].  
  
## <a name="create-a-sharepoint-project"></a>Criar um projeto do SharePoint
 Primeiro, crie um projeto do SharePoint.  
  
#### <a name="to-create-a-sharepoint-project"></a>Para criar um projeto do SharePoint  
  
1. Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.  
  
2. Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3. No painel modelos, escolha o **projeto do SharePoint 2010** modelo.  
  
4. No **nome** , digite **ProfileTest**e, em seguida, escolha o **Okey** botão.  
  
    O **Assistente para personalização do SharePoint** é exibida.  
  
5. Sobre o **especificar o nível de site e segurança para depuração** página, insira a URL do servidor do site do SharePoint onde você deseja depurar a definição de site ou usar o local padrão (http://<em>nome do sistema</em>/) .  
  
6. No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção.  
  
    No momento, você pode apenas soluções de farm de perfil. Para obter mais informações sobre soluções em área restrita em comparação com soluções de farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
7. Escolha o **concluir** botão. O projeto aparece na **Gerenciador de soluções**.  
  
## <a name="add-a-feature-and-feature-event-receiver"></a>Adicionar um recurso e o receptor de evento de recurso
 Em seguida, adicione um recurso para o projeto, juntamente com um receptor de eventos para o recurso. Esse receptor de evento conterá o código para criação de perfil.  
  
#### <a name="to-add-a-feature-and-feature-event-receiver"></a>Para adicionar um recurso e o receptor de evento de recurso  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **recursos** nó, escolha **adicionar recurso**e deixe o nome com o valor padrão, **Feature1**.  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho **Feature1**e, em seguida, escolha **adicionar receptor de evento**.  
  
     Isso adiciona um arquivo de código para o recurso com vários manipuladores de eventos comentada e abre o arquivo para edição.  
  
3.  Na classe de receptor de evento, adicione as seguintes declarações de variável.  
  
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
  
4.  Substitua o `FeatureActivated` procedimento com o código a seguir.  
  
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
  
5.  Adicione o seguinte procedimento abaixo o `FeatureActivated`procedimento.  
  
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
  
6.  Na **Gerenciador de soluções**, abra o menu de atalho para o projeto (**ProfileTest**) e, em seguida, escolha **propriedades**.  
  
7.  No **propriedades** diálogo caixa, escolha o **SharePoint** guia.  
  
8.  No **configuração de implantação ativa** , escolha **sem ativação**.  
  
     Selecionar essa configuração de implantação permite que você ativar manualmente o recurso mais tarde no SharePoint.  
  
9. Salvar o projeto.  
  
## <a name="configure-and-deploy-the-sharepoint-application"></a>Configurar e implantar o aplicativo do SharePoint
 Agora que o projeto do SharePoint estiver pronto, configurá-lo e implantá-lo no servidor do SharePoint.  
  
#### <a name="to-configure-and-deploy-the-sharepoint-application"></a>Para configurar e implantar o aplicativo do SharePoint  
  
1.  Sobre o **Analyze** menu, escolha **Launch Performance Wizard**.  
  
2.  Na página do **Performance Wizard**, deixe o método de criação de perfil como **amostragem de CPU** e escolha o **próxima** botão.  
  
     Os outros métodos de criação de perfil podem ser usados em mais avançados de situações de criação de perfil. Para obter mais informações, consulte [Noções Básicas sobre Métodos de Coleta de Desempenho](/visualstudio/profiling/understanding-performance-collection-methods).  
  
3.  Na página dois dos **Performance Wizard**, deixe o perfil de destino como **ProfileTest** e escolha o **próxima** botão.  
  
     Se uma solução tem vários projetos, elas aparecem nessa lista.  
  
4.  Na página três da **Performance Wizard**, desmarque a **habilitar Tier Interaction Profiling** caixa de seleção e, em seguida, escolha o **próxima** botão.  
  
     O recurso de criação de perfil de interação de camada (TIP) é útil para medir o desempenho de aplicativos que consultar bancos de dados e para mostrar a você o número de vezes que uma página da web é solicitada. Como esses dados não são necessários para este exemplo, podemos não habilitará esse recurso.  
  
5.  Na página quatro a **Performance Wizard**, deixe o **iniciar após a conclusão do Assistente de criação de perfil** selecionada de caixa de seleção e, em seguida, escolha o **concluir** botão.  
  
     O assistente permite a criação de perfil de aplicativo no servidor, exibe a **Performance Explorer** janela e, em seguida, compilações, implanta e executa o aplicativo do SharePoint.  
  
## <a name="run-the-sharepoint-application"></a>Executar o aplicativo do SharePoint
 Ativar o recurso no SharePoint, disparando o `FeatureActivation` código de evento para ser executado.  
  
#### <a name="to-run-the-sharepoint-application"></a>Para executar o aplicativo do SharePoint  
  
1.  No SharePoint, abra o **ações do Site** menu e, em seguida, escolha **configurações de Site**.  
  
2.  No **ações do Site** , escolha o **gerenciar recursos do site** link.  
  
3.  No **recursos** , escolha o **ativar** lado **ProfileTest Feature1**.  
  
     Há uma pausa quando você fizer isso, devido ao loop ocioso que está sendo chamado no `FeatureActivated` função.  
  
4.  No **início rápido** barra, escolha **lista** e, em seguida, no **lista** , escolha **anúncios**.  
  
     Observe que um novo aviso foi adicionado à lista informando que o recurso foi ativado.  
  
5.  Feche o site do SharePoint.  
  
     Depois de fechar o SharePoint, o criador de perfil cria e exibe um relatório de criação de perfil de exemplo e salva-o como um arquivo. vsp na **ProfileTest** pasta do projeto.  
  
## <a name="view-and-interpret-the-profile-results"></a>Exibir e interpretar os resultados de perfil
 Agora que você executou e criação de perfil de aplicativo do SharePoint, exiba os resultados de teste.  
  
#### <a name="to-view-and-interpret-the-profile-results"></a>Para exibir e interpretar os resultados de perfil
  
1.  No **funções que realizam o trabalho mais Individual** seção do relatório de criação de perfil de exemplo, observe que `TimeCounter` está no topo da lista.  
  
     Esse local indica que `TimeCounter` foi uma das funções com o maior número de amostras, significando que é um dos afunilamentos de desempenho maiores no aplicativo. Essa situação não é surpreendente, no entanto, porque ela era propositadamente projetado dessa forma, para fins de demonstração.  
  
2.  No **funções que realizam o trabalho mais Individual** , escolha o `ProcessRequest` link para exibir a distribuição de custo para o `ProcessRequest` função.  
  
     No **funções chamadas** seção para o `ProcessRequest`, observe que o **FeatureActiviated** função é listada como os mais caros chamada de função.  
  
3.  No **funções chamadas** , escolha o **FeatureActivated** botão.  
  
     No **funções chamadas** seção **FeatureActivated**, o `TimeCounter` função é listada como os mais caros chamada de função. No **modo de exibição de código de função** painel, o código realçado (`TimeCounter`) é o ponto de acesso e indica onde a correção é necessária.  
  
4.  Feche o relatório de criação de perfil de exemplo.  
  
     Para exibir o relatório novamente a qualquer momento, abra o arquivo. vsp na **Performance Explorer** janela.  
  
## <a name="fix-the-code-and-reprofile-the-application"></a>Corrija o código e reprofile o aplicativo
 Agora que a função de ponto de acesso no aplicativo do SharePoint tiver sido identificada, corrigi-lo.  
  
#### <a name="to-fix-the-code-and-reprofile-the-application"></a>Para corrigir o código e reprofile o aplicativo  
  
1.  Em que o código de receptor de evento de recurso, comente a `TimeCounter` chamada de método na `FeatureActivated` impedi-lo de que está sendo chamado.  
  
2.  Salvar o projeto.  
  
3.  Na **Gerenciador de desempenho**, abra a pasta de destino e, em seguida, escolha o **ProfileTest** nó.  
  
4.  No **Gerenciador de desempenho** barra de ferramentas, no **ações** guia, escolha o **Iniciar criação de perfil** botão.  
  
     Se você quiser alterar qualquer uma das propriedades de criação de perfil antes de reprofiling o aplicativo, escolha o **Launch Performance Wizard** botão em vez disso.  
  
5.  Siga as instruções de **executando o aplicativo do SharePoint** seção, anteriormente neste tópico.  
  
     O recurso deve ativar muito mais rapidamente agora que a chamada para o loop ocioso foi eliminada. O exemplo de relatório de criação de perfil deve refletir isso.  
  
## <a name="see-also"></a>Consulte também
 [Gerenciador de Desempenho](/visualstudio/profiling/performance-explorer)   
 [Visão geral da sessão de desempenho](/visualstudio/profiling/performance-session-overview)   
 [Guia do iniciante à criação de perfil do desempenho](/visualstudio/profiling/beginners-guide-to-performance-profiling)   
 [Encontre afunilamentos de aplicativos com o Visual Studio Profiler](http://go.microsoft.com/fwlink/?LinkID=137266)  
  
