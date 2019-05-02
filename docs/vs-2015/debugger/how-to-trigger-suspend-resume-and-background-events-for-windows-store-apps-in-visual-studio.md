---
title: Como disparar suspender, continuar e eventos para aplicativos da Windows Store em segundo plano
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.background_task_activate_failure
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 824ff3ca-fedf-4cf5-b3e2-ac8dc82d40ac
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ecf43708b854ebee444d2117bc32df41907118a3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442722"
---
# <a name="how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio"></a>Como disparar eventos de suspensão, retomada e segundo plano para aplicativos da Windows Store no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você não está depurando, o **PLM (Gerenciamento de Tempo de Vida do Processo)** do Windows controla o estado da execução de seu aplicativo, iniciando, suspendendo, retomando e encerrando o aplicativo em resposta às ações do usuário e ao estado do dispositivo. Quando você está depurando, o Windows desabilita esses eventos de ativação. Este tópico descreve como acionar esses eventos no depurador.

 Este tópico também descreve como depurar **Tarefas em segundo plano**. Essas tarefas permitem que você execute certas operações em um processo em segundo plano, mesmo quando o aplicativo não está sendo executado. Você pode usar o depurador para colocar o aplicativo no modo de depuração e depois, sem iniciar a interface de usuário, iniciar e depurar a tarefa em segundo plano.

 Para obter mais informações sobre tarefas de gerenciamento de tempo de vida do processo e em segundo plano, consulte [Iniciar, retomar e multitarefa](http://msdn.microsoft.com/04307b1b-05af-46a6-b639-3f35e297f71b).

## <a name="BKMK_In_this_topic"></a> Neste tópico
 [Eventos de gerenciamento de tempo de vida do processo de gatilho](#BKMK_Trigger_Process_Lifecycle_Management_events)

 [Tarefas em segundo plano de gatilho](#BKMK_Trigger_background_tasks)

- [Disparar um evento de tarefa do plano de fundo de uma sessão de depuração padrão](#BKMK_Trigger_a_background_task_event_from_a_standard_debug_session)

- [Disparar uma tarefa em segundo plano quando o aplicativo não está em execução](#BKMK_Trigger_a_background_task_when_the_app_is_not_running)

  [Disparar eventos de gerenciamento de tempo de vida de processos e tarefas de um aplicativo instalado em segundo plano](#BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app)

  [Diagnosticando erros de ativação de tarefa em segundo plano](#BKMK_Diagnosing_background_task_activation_errors)

## <a name="BKMK_Trigger_Process_Lifecycle_Management_events"></a> Disparar eventos de gerenciamento de tempo de vida do processo
 O Windows pode suspender o aplicativo quando o usuário sai dele ou quando o Windows entra em um estado de baixo consumo de energia. Você pode responder ao evento `Suspending` para salvar dados relevantes do aplicativo e do usuário em um armazenamento persistente e para liberar recursos. Quando um aplicativo é retomado do estado **Suspenso**, ele entra no estado **De Execução** e continua de onde estava quando foi suspenso. Você pode responder ao evento `Resuming` para restaurar ou atualizar o estado do aplicativo e recuperar recursos.

 Embora o Windows tente manter o máximo possível de aplicativos suspensos na memória, ele poderá terminar o aplicativo se não houver recursos suficientes para mantê-lo na memória. Um usuário também pode fechar o aplicativo explicitamente. Não há nenhum evento especial para indicar que o usuário fechou um aplicativo.

 No depurador do Visual Studio, você pode manualmente suspender, retomar e terminar seus aplicativos para depurar eventos do ciclo de vida do processo. Para depurar um evento do ciclo de vida do processo:

1. Defina um ponto de interrupção no manipulador do evento que você deseja depurar.

2. Pressione **F5** para iniciar a depuração.

3. Na barra de ferramentas **Local de Depuração**, escolha o evento que deseja acionar:

     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

     Observe que **Suspender e Encerrar** fecha o aplicativo e encerra a sessão de depuração.

## <a name="BKMK_Trigger_background_tasks"></a> Disparar tarefas em segundo plano
 Qualquer aplicativo pode registrar uma tarefa em segundo plano para responder a determinados eventos do sistema, mesmo quando o aplicativo não está sendo executado. As tarefas em segundo plano não podem executar o código que atualiza diretamente a interface do usuário; em vez disso, elas mostram informações para o usuário com atualizações de bloco, atualizações de notificação e notificações do sistema. Para obter mais informações, consulte [que dão suporte a seu aplicativo com tarefas em segundo plano](http://msdn.microsoft.com/4c7bb148-eb1f-4640-865e-41f627a46e8e)

 Você pode disparar os eventos que iniciam as tarefas em segundo plano do aplicativo por meio do depurador.

> [!NOTE]
> O depurador só pode disparar os eventos que não contêm dados, como os que indicam uma alteração de estado no dispositivo. Você precisa disparar manualmente as tarefas em segundo plano que exigem a entrada do usuário ou outros dados.

 A maneira mais realística de disparar um evento de tarefa em segundo plano é quando o aplicativo não está sendo executado. No entanto, também é possível disparar o evento em uma sessão de depuração padrão.

### <a name="BKMK_Trigger_a_background_task_event_from_a_standard_debug_session"></a> Disparar um evento de tarefa em segundo plano de uma sessão de depuração padrão

1. Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.

2. Pressione **F5** para iniciar a depuração.

3. Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.

     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

### <a name="BKMK_Trigger_a_background_task_when_the_app_is_not_running"></a> Disparar uma tarefa em segundo plano quando o aplicativo não está em execução

1. Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.

2. Abra a página de propriedades de depuração do projeto de inicialização. No Gerenciador de Soluções, selecione o projeto. No menu **Depurar**, escolha **Propriedades**.

     Para projetos C++, talvez seja necessário expandir **propriedades de configuração** e, em seguida, escolha **depuração**.

3. Realize um dos seguintes procedimentos:

    - Para projetos em Visual C# e Visual Basic, escolha **Não iniciar, mas depurar meu código quando ele for iniciado**

         ![C&#35;&#47;propriedade de aplicativo de inicialização de depuração VB](../debugger/media/dbg-csvb-dontlaunchapp.png "DBG_CsVb_DontLaunchApp")

    - Para projetos em JavaScript e Visual C++, escolha **Não** na lista **Iniciar aplicativo**.

         ![C&#43;&#43;&#47;propriedade de depuração do aplicativo inicie VB](../debugger/media/dbg-cppjs-dontlaunchapp.png "DBG_CppJs_DontLaunchApp")

4. Pressione **F5** para colocar o aplicativo no modo de depuração. Observe que a lista **Processo** na barra de ferramentas **Local de Depuração** exibe o nome do pacote do aplicativo para indicar que você está no modo de depuração.

     ![Lista de processos de tarefa em segundo plano](../debugger/media/dbg-backgroundtask-processlist.png "DBG_BackgroundTask_ProcessList")

5. Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.

     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

## <a name="BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app"></a> Disparar eventos de gerenciamento de tempo de vida do processo e tarefas em segundo plano de um aplicativo instalado
 Use a caixa de diálogo Depurar Aplicativo Instalado para carregar um aplicativo que já está instalado no depurador. Por exemplo, você pode depurar um aplicativo instalado da Windows Store ou depurar um aplicativo quando tiver seus arquivos de origem, mas não um projeto do Visual Studio para o aplicativo. A caixa de diálogo Depurar Aplicativo Instalado permite que você inicie um aplicativo no modo de depuração no computador do Visual Studio ou em um dispositivo remoto, ou que você defina que o aplicativo seja executado no modo de depuração, mas não seja iniciado. Consulte a **iniciar um aplicativo instalado no depurador** seção de um a [JavaScript](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md#BKMK_Start_an_installed_app_in_the_debugger) ou [Visual C++, Visual c# e Visual Basic](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md#BKMK_Start_an_installed_app_in_the_debugger) versões do **como iniciar uma sessão de depuração** para obter mais informações.

 Após o aplicativo ser carregado no depurador, você poderá executar qualquer um dos procedimentos acima.

## <a name="BKMK_Diagnosing_background_task_activation_errors"></a> Diagnosticando erros de ativação de tarefa em segundo plano
 Os logs de diagnóstico no Visualizador de Eventos do Windows referentes à infraestrutura em segundo plano contêm informações detalhadas que podem ser usadas para diagnosticar e solucionar erros de tarefas em segundo plano. Para exibir o log:

1. Abra o aplicativo visualizador de eventos.

2. No painel **Ações**, escolha **Exibir** e verifique se **Mostrar logs analíticos e de depuração** está marcado.

3. Sobre o **Visualizador de eventos (Local)** de árvore, expanda os nós **Applications and Services Logs** / **Microsoft** / **Windows**   /  **BackgroundTasksInfrastructure**.

4. Escolha o log **Diagnóstico**.

## <a name="see-also"></a>Consulte também
 [Testando aplicativos da Store com o Visual Studio](../test/testing-store-apps-with-visual-studio.md) [depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md) [ciclo de vida do aplicativo](http://msdn.microsoft.com/53cdc987-c547-49d1-a5a4-fd3f96b2259d) [iniciando, retomar e multitarefa](http://msdn.microsoft.com/04307b1b-05af-46a6-b639-3f35e297f71b)
