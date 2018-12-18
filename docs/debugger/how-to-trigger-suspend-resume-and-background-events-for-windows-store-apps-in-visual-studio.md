---
title: Gatilho de suspender, continuar e eventos em segundo plano durante a depuração UWP | Microsoft Docs
ms.custom: seodec18
ms.date: 01/16/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.background_task_activate_failure
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 8d467d19a55d47ccfa231bef2b473fa5be405921
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53054655"
---
# <a name="how-to-trigger-suspend-resume-and-background-events-while-debugging-uwp-apps-in-visual-studio"></a>Como disparar suspender, continuar e eventos em segundo plano durante a depuração de aplicativos UWP no Visual Studio
Quando você não está depurando, o **PLM (Gerenciamento de Tempo de Vida do Processo)** do Windows controla o estado da execução de seu aplicativo, iniciando, suspendendo, retomando e encerrando o aplicativo em resposta às ações do usuário e ao estado do dispositivo. Quando você está depurando, o Windows desabilita esses eventos de ativação. Este tópico descreve como acionar esses eventos no depurador.  
  
 Este tópico também descreve como depurar **Tarefas em segundo plano**. Essas tarefas permitem que você execute certas operações em um processo em segundo plano, mesmo quando o aplicativo não está sendo executado. Você pode usar o depurador para colocar o aplicativo no modo de depuração e depois, sem iniciar a interface de usuário, iniciar e depurar a tarefa em segundo plano.  
  
 Para obter mais informações sobre tarefas de gerenciamento de tempo de vida do processo e em segundo plano, consulte [Iniciar, retomar e multitarefa](/windows/uwp/launch-resume/index).  
  
##  <a name="BKMK_Trigger_Process_Lifecycle_Management_events"></a> Disparar eventos de gerenciamento de tempo de vida do processo  
 O Windows pode suspender o aplicativo quando o usuário sai dele ou quando o Windows entra em um estado de baixo consumo de energia. Você pode responder ao evento `Suspending` para salvar dados relevantes do aplicativo e do usuário em um armazenamento persistente e para liberar recursos. Quando um aplicativo é retomado do estado **Suspenso**, ele entra no estado **De Execução** e continua de onde estava quando foi suspenso. Você pode responder ao evento `Resuming` para restaurar ou atualizar o estado do aplicativo e recuperar recursos.  
  
 Embora o Windows tente manter o máximo possível de aplicativos suspensos na memória, ele poderá terminar o aplicativo se não houver recursos suficientes para mantê-lo na memória. Um usuário também pode fechar o aplicativo explicitamente. Não há nenhum evento especial para indicar que o usuário fechou um aplicativo.  
  
 No depurador do Visual Studio, você pode manualmente suspender, retomar e terminar seus aplicativos para depurar eventos do ciclo de vida do processo. Para depurar um evento do ciclo de vida do processo:  
  
1.  Defina um ponto de interrupção no manipulador do evento que você deseja depurar.  
  
2.  Pressione **F5** para iniciar a depuração.  
  
3.  Na barra de ferramentas **Local de Depuração**, escolha o evento que deseja acionar:  
  
     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg_suspendresumebackground.png "DBG_SuspendResumeBackground")  
  
     Observe que **Suspender e Encerrar** fecha o aplicativo e encerra a sessão de depuração.  
  
##  <a name="BKMK_Trigger_background_tasks"></a> Disparar tarefas em segundo plano  
 Qualquer aplicativo pode registrar uma tarefa em segundo plano para responder a determinados eventos do sistema, mesmo quando o aplicativo não está sendo executado. As tarefas em segundo plano não podem executar o código que atualiza diretamente a interface do usuário; em vez disso, elas mostram informações para o usuário com atualizações de bloco, atualizações de notificação e notificações do sistema. Para obter mais informações, consulte [que dão suporte a seu aplicativo com tarefas em segundo plano](https://msdn.microsoft.com/library/4c7bb148-eb1f-4640-865e-41f627a46e8e)  
  
 Você pode disparar os eventos que iniciam as tarefas em segundo plano do aplicativo por meio do depurador.  
  
> [!NOTE]
>  O depurador só pode disparar os eventos que não contêm dados, como os que indicam uma alteração de estado no dispositivo. Você precisa disparar manualmente as tarefas em segundo plano que exigem a entrada do usuário ou outros dados.  
  
 A maneira mais realística de disparar um evento de tarefa em segundo plano é quando o aplicativo não está sendo executado. No entanto, também é possível disparar o evento em uma sessão de depuração padrão.  
  
###  <a name="BKMK_Trigger_a_background_task_event_from_a_standard_debug_session"></a> Disparar um evento de tarefa em segundo plano de uma sessão de depuração padrão  
  
1.  Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.  
  
2.  Pressione **F5** para iniciar a depuração.  
  
3.  Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.  
  
     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg_suspendresumebackground.png "DBG_SuspendResumeBackground")  
  
###  <a name="BKMK_Trigger_a_background_task_when_the_app_is_not_running"></a> Disparar uma tarefa em segundo plano quando o aplicativo não está em execução  
  
1.  Defina um ponto de interrupção no código de tarefa em segundo plano que você deseja depurar.  
  
2.  Abra a página de propriedades de depuração do projeto de inicialização. No Gerenciador de Soluções, selecione o projeto. No menu **Depurar**, escolha **Propriedades**.  
  
     Para projetos C++ e JavaScript, expanda **propriedades de configuração** e, em seguida, escolha **depuração**.  
  
3.  Realize um dos seguintes procedimentos:  
  
    -   Para projetos em Visual C# e Visual Basic, escolha **Não iniciar, mas depurar meu código quando ele for iniciado**  
  
         ![C&#35;&#47;propriedade de aplicativo de inicialização de depuração VB](../debugger/media/dbg_csvb_dontlaunchapp.png "DBG_CsVb_DontLaunchApp")  
  
    -   Para projetos em JavaScript e Visual C++, escolha **Não** na lista **Iniciar aplicativo**.  
  
         ![C&#43;&#43;&#47;propriedade de depuração do aplicativo inicie VB](../debugger/media/dbg_cppjs_dontlaunchapp.png "DBG_CppJs_DontLaunchApp")  
  
4.  Pressione **F5** para colocar o aplicativo no modo de depuração. Observe que a lista **Processo** na barra de ferramentas **Local de Depuração** exibe o nome do pacote do aplicativo para indicar que você está no modo de depuração.  
  
     ![Lista de processos de tarefa em segundo plano](../debugger/media/dbg_backgroundtask_processlist.png "DBG_BackgroundTask_ProcessList")  
  
5.  Na lista de eventos na barra de ferramentas **Local de Depuração**, escolha a tarefa em segundo plano que você deseja iniciar.  
  
     ![Suspender, retomar, encerrar e tarefas em segundo plano](../debugger/media/dbg_suspendresumebackground.png "DBG_SuspendResumeBackground")  
  
##  <a name="BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app"></a> Disparar eventos de gerenciamento de tempo de vida do processo e tarefas em segundo plano de um aplicativo instalado  
 Use o **depurar pacote do aplicativo instalado** caixa de diálogo para carregar um aplicativo que já está instalado no depurador. Por exemplo, você pode depurar um aplicativo que tenha sido instalado na Microsoft Store ou depurar um aplicativo quando você tem os arquivos de origem para o aplicativo, mas não um projeto do Visual Studio para o aplicativo. O **depurar pacote do aplicativo instalado** caixa de diálogo permite que você inicia um aplicativo no modo de depuração na máquina do Visual Studio ou em um dispositivo remoto, ou para definir o aplicativo seja executado no modo de depuração, mas não iniciá-lo. Para obter mais informações, consulte [depurar pacote de aplicativo instalado](../debugger/debug-installed-app-package.md).
  
 Após o aplicativo ser carregado no depurador, você poderá executar qualquer um dos procedimentos acima.  
  
##  <a name="BKMK_Diagnosing_background_task_activation_errors"></a> Diagnosticando erros de ativação de tarefa em segundo plano  
 Os logs de diagnóstico no Visualizador de Eventos do Windows referentes à infraestrutura em segundo plano contêm informações detalhadas que podem ser usadas para diagnosticar e solucionar erros de tarefas em segundo plano. Para exibir o log:  
  
1.  Abra o aplicativo visualizador de eventos.  
  
2.  No painel **Ações**, escolha **Exibir** e verifique se **Mostrar logs analíticos e de depuração** está marcado.  
  
3.  Sobre o **Visualizador de eventos (Local)** de árvore, expanda os nós **Applications and Services Logs** > **Microsoft** > **Windows**   >  **BackgroundTasksInfrastructure**.  
  
4.  Escolha o log **Diagnóstico**.  
  
## <a name="see-also"></a>Consulte também  
 [Testando aplicativos UWP com o Visual Studio](../test/testing-store-apps-with-visual-studio.md)   
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)   
 [Ciclo de vida do aplicativo](/windows/uwp/launch-resume/app-lifecycle)   
 [Iniciando, retomar e execução multitarefa](/windows/uwp/launch-resume/index)