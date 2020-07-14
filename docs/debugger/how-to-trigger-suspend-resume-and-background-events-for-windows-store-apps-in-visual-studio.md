---
title: Disparar eventos de suspensão/retomada/segundo plano ao depurar UWP
ms.custom: seodec18
ms.date: 01/16/2018
ms.topic: how-to
f1_keywords:
- vs.debug.error.background_task_activate_failure
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 83b4bea32f642cbf48acb01831bd4bccc2bb15a0
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348932"
---
# <a name="how-to-trigger-suspend-resume-and-background-events-while-debugging-uwp-apps-in-visual-studio"></a>Como disparar eventos de suspensão, retomada e segundo plano durante a depuração de aplicativos UWP no Visual Studio

Quando você não está depurando, o **PLM (Gerenciamento de Tempo de Vida do Processo)** do Windows controla o estado da execução de seu aplicativo, iniciando, suspendendo, retomando e encerrando o aplicativo em resposta às ações do usuário e ao estado do dispositivo. Quando você está depurando, o Windows desabilita esses eventos de ativação. Este tópico descreve como acionar esses eventos no depurador.

Este tópico também descreve como depurar **Tarefas em segundo plano**. As tarefas em segundo plano permitem que você execute determinadas operações em um processo em segundo plano, mesmo quando seu aplicativo não está em execução. Você pode usar o depurador para colocar o aplicativo no modo de depuração e depois, sem iniciar a interface de usuário, iniciar e depurar a tarefa em segundo plano.

Para obter mais informações sobre o gerenciamento de tempo de vida de processos e tarefas em segundo plano, consulte [iniciando, retomando e multitarefa](/windows/uwp/launch-resume/index).

## <a name="trigger-process-lifetime-management-events"></a><a name="BKMK_Trigger_Process_Lifecycle_Management_events"></a> Disparar eventos de gerenciamento de tempo de vida do processo
 O Windows pode suspender seu aplicativo quando o usuário sai dele ou quando o Windows entra em um estado de baixa energia. Você pode responder ao evento `Suspending` para salvar dados relevantes do aplicativo e do usuário em um armazenamento persistente e para liberar recursos. Quando um aplicativo é retomado do estado **Suspenso**, ele entra no estado **De Execução** e continua de onde estava quando foi suspenso. Você pode responder ao evento `Resuming` para restaurar ou atualizar o estado do aplicativo e recuperar recursos.

 Embora o Windows tente manter o máximo possível de aplicativos suspensos na memória, ele poderá terminar o aplicativo se não houver recursos suficientes para mantê-lo na memória. Um usuário também pode fechar o aplicativo explicitamente. Não há nenhum evento especial para indicar que o usuário fechou um aplicativo.

 No depurador do Visual Studio, você pode manualmente suspender, retomar e terminar seus aplicativos para depurar eventos do ciclo de vida do processo. Para depurar um evento do ciclo de vida do processo:

1. Defina um ponto de interrupção no manipulador do evento que você deseja depurar.

2. Pressione **F5** para iniciar a depuração.

3. Na barra de ferramentas **Local de Depuração**, escolha o evento que deseja acionar:

     ![Tarefas de suspender, retomar, encerrar e em segundo plano](../debugger/media/dbg_suspendresumebackground.png)

     **Suspender e encerrar** fecha o aplicativo e encerra a sessão de depuração.

## <a name="trigger-background-tasks"></a><a name="BKMK_Trigger_background_tasks"></a> Disparar tarefas em segundo plano
 Qualquer aplicativo pode registrar uma tarefa em segundo plano para responder a determinados eventos do sistema, mesmo quando o aplicativo não está sendo executado. As tarefas em segundo plano não podem executar o código que atualiza diretamente a interface do usuário; em vez disso, elas mostram informações para o usuário com atualizações de bloco, atualizações de notificação e notificações do sistema. Para obter mais informações, consulte [dando suporte ao seu aplicativo com tarefas em segundo plano](https://msdn.microsoft.com/library/4c7bb148-eb1f-4640-865e-41f627a46e8e).

 Você pode disparar os eventos que iniciam as tarefas em segundo plano do aplicativo por meio do depurador.

> [!NOTE]
> O depurador só pode disparar os eventos que não contêm dados, como os que indicam uma alteração de estado no dispositivo. Você precisa disparar manualmente as tarefas em segundo plano que exigem a entrada do usuário ou outros dados.

 A maneira mais realística de disparar um evento de tarefa em segundo plano é quando o aplicativo não está sendo executado. No entanto, também é possível disparar o evento em uma sessão de depuração padrão.

### <a name="trigger-a-background-task-event-from-a-standard-debug-session"></a><a name="BKMK_Trigger_a_background_task_event_from_a_standard_debug_session"></a> Disparar um evento de tarefa em segundo plano de uma sessão de depuração padrão

1. Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.

2. Pressione **F5** para iniciar a depuração.

3. Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.

     ![Tarefas de suspender, retomar, encerrar e em segundo plano](../debugger/media/dbg_suspendresumebackground.png)

### <a name="trigger-a-background-task-when-the-app-is-not-running"></a><a name="BKMK_Trigger_a_background_task_when_the_app_is_not_running"></a> Disparar uma tarefa em segundo plano quando o aplicativo não está em execução

1. Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.

2. Abra a página de propriedades de depuração do projeto de inicialização. No Gerenciador de Soluções, selecione o projeto. No menu **Depurar**, escolha **Propriedades**.

     Para projetos C++, expanda **Propriedades de configuração** e escolha **depuração**.

3. Realize um dos seguintes procedimentos:

    - Para projetos em Visual C# e Visual Basic, escolha **Não iniciar, mas depurar meu código quando ele for iniciado**

         ![Propriedade do aplicativo inicialização de depuração do C&#35;&#47;VB](../debugger/media/dbg_csvb_dontlaunchapp.png "DBG_CsVb_DontLaunchApp")

    - Para projetos C++, escolha **não** na lista **Iniciar aplicativo** .

         ![C&#43;&#43;&#47;VB iniciar a propriedade de depuração do aplicativo](../debugger/media/dbg_cppjs_dontlaunchapp.png "DBG_CppJs_DontLaunchApp")

4. Pressione **F5** para colocar o aplicativo no modo de depuração. Observe que a lista **Processo** na barra de ferramentas **Local de Depuração** exibe o nome do pacote do aplicativo para indicar que você está no modo de depuração.

     ![Lista de processos da tarefa em segundo plano](../debugger/media/dbg_backgroundtask_processlist.png "DBG_BackgroundTask_ProcessList")

5. Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.

     ![Tarefas de suspender, retomar, encerrar e em segundo plano](../debugger/media/dbg_suspendresumebackground.png "DBG_SuspendResumeBackground")

## <a name="trigger-process-lifetime-management-events-and-background-tasks-from-an-installed-app"></a><a name="BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app"></a> Disparar eventos de gerenciamento de tempo de vida do processo e tarefas em segundo plano de um aplicativo instalado
 Use a caixa de diálogo **depurar pacote do aplicativo instalado** para carregar um aplicativo que já está instalado no depurador. Por exemplo, você pode depurar um aplicativo que foi instalado de Microsoft Store ou depurar um aplicativo quando tiver os arquivos de origem para o aplicativo, mas não um projeto do Visual Studio para o aplicativo. A caixa de diálogo **depurar pacote do aplicativo instalado** permite iniciar um aplicativo no modo de depuração no computador do Visual Studio ou em um dispositivo remoto, ou para definir o aplicativo para ser executado no modo de depuração, mas não iniciá-lo. Para obter mais informações, consulte [depurar um pacote do aplicativo instalado](../debugger/debug-installed-app-package.md).

 Após o aplicativo ser carregado no depurador, você poderá executar qualquer um dos procedimentos acima.

## <a name="diagnosing-background-task-activation-errors"></a><a name="BKMK_Diagnosing_background_task_activation_errors"></a> Diagnosticando erros de ativação de tarefa em segundo plano
 Os logs de diagnóstico no Windows Visualizador de Eventos para a infraestrutura em segundo plano contêm informações detalhadas que você pode usar para diagnosticar e solucionar problemas de erros de tarefas em segundo plano. Para exibir o log:

1. Abra o aplicativo visualizador de eventos.

2. No painel **Ações**, escolha **Exibir** e verifique se **Mostrar logs analíticos e de depuração** está marcado.

3. Na árvore **Visualizador de eventos (local)** , expanda os nós **aplicativos e logs de serviços**  >  **Microsoft**  >  **Windows**  >  **BackgroundTasksInfrastructure**.

4. Escolha o log **Diagnóstico**.

## <a name="see-also"></a>Veja também
- [Testando aplicativos UWP com o Visual Studio](/visualstudio/test/create-and-run-unit-tests-for-a-store-app-in-visual-studio)
- [Depurar aplicativos no Visual Studio](debugging-windows-store-and-windows-universal-apps.md)
- [Ciclo de vida do aplicativo](/windows/uwp/launch-resume/app-lifecycle)
- [Inicialização, continuação e multitarefa](/windows/uwp/launch-resume/index)