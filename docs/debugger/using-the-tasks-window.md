---
title: Usando a janela tarefas | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.paralleltasks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: bd5e0612-a0dc-41cf-a7af-1e87d0d5c35f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6d22202e50c973c52bf2b47374b9eda583fb3fe8
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44280877"
---
# <a name="using-the-tasks-window"></a>Usando a janela Tarefas

O **tarefas** janela se parece com o **Threads** janela, exceto que mostra informações sobre <xref:System.Threading.Tasks.Task?displayProperty=fullName>, [task_handle](/cpp/parallel/concrt/reference/task-group-class), ou [WinJS. Promise ](/previous-versions/windows/apps/br211867(v=win.10)) objetos em vez de cada thread. Como threads, as tarefas representam as operações assíncronas que podem ser executadas simultaneamente; no entanto, várias tarefas podem ser executadas no mesmo thread.

No código gerenciado, você pode usar o **tarefas** janela quando você trabalha com <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos ou com o **await** e **async** palavras-chave (**Await** e **Async** no Visual Basic). Para obter mais informações sobre as tarefas no código gerenciado, consulte [programação paralela](/dotnet/standard/parallel-programming/index).

No código nativo, você pode usar o **tarefas** janela quando você trabalha com [grupos de tarefas](/cpp/parallel/concrt/task-parallelism-concurrency-runtime), [algoritmos em paralelo](/cpp/parallel/concrt/parallel-algorithms), [agentes assíncronos](/cpp/parallel/concrt/asynchronous-agents), e [tarefas leves](/cpp/parallel/concrt/task-scheduler-concurrency-runtime). Para obter mais informações sobre as tarefas no código nativo, consulte [tempo de execução de simultaneidade](/cpp/parallel/concrt/concurrency-runtime).

No JavaScript, você pode usar a janela tarefas quando você estiver trabalhando com a promessa `.then` código. Ver [programação assíncrona em JavaScript (aplicativos UWP)](/previous-versions/windows/apps/hh700330(v=win.10)) para obter mais informações.

Você pode usar o **tarefas** janela sempre que você invadir o depurador. Você pode acessá-lo na **Debug** menu clicando **Windows** e, em seguida, clicando em **tarefas**. A ilustração a seguir mostra a **tarefas** janela no modo padrão.

![Janela tarefas](../debugger/media/parallel_tasks_window.png "Parallel_Tasks_Window")

> [!NOTE]
> No código gerenciado, uma <xref:System.Threading.Tasks.Task> que tem um status de [TaskStatus.Created](<xref:System.Threading.Tasks.TaskStatus.Created>), [TaskStatus.WaitingForActivation](<xref:System.Threading.Tasks.TaskStatus.WaitingForActivation>), ou [TaskStatus.WaitingToRun](<xref:System.Threading.Tasks.TaskStatus.WaitingToRun>) pode não ser exibido na **tarefas** janela quando os threads gerenciados estão em um estado de suspensão ou junção.

## <a name="tasks-column-information"></a>Informações da coluna de tarefas

As colunas na **tarefas** janela Mostrar as informações a seguir.

|Nome da coluna|Descrição|
|-----------------|-----------------|
|**sinalizadores**|Mostra quais tarefas estão sinalizadas e permite sinalizar ou remover a sinalização de uma tarefa.|
|**Ícones**|Uma seta amarela indica a tarefa atual. A tarefa atual é a tarefa mais alta no thread atual.<br /><br /> Uma seta branca indica a tarefa de quebra, isto é, a que era atual quando o depurador foi chamado.<br /><br /> O ícone de pausa indica uma tarefa que foi congelada pelo usuário. Você pode congelar e descongelar uma tarefa clicando com o botão direito na lista.|
|**ID**|Um número fornecido pelo sistema para a tarefa. No código nativo, esse é o endereço da tarefa.|
|**Status**|O estado atual (agendado, ativo, bloqueado, com deadlock, aguardando ou concluído) da tarefa. Uma tarefa agendada é aquela que ainda não foi executada e, portanto, ainda não tem uma pilha de chamadas, um thread alocado ou as informações relacionadas.<br /><br /> Uma tarefa ativa é aquela que estava executando o código antes de quebrar no depurador.<br /><br /> Uma tarefa aguardando ou bloqueada é aquele que está bloqueada porque está aguardando um evento ser sinalizado, um bloqueio ser liberado ou outra tarefa ser concluída.<br /><br /> Uma tarefa com deadlock é uma tarefa de espera cujo thread está bloqueado com outro thread.<br /><br /> Passe o mouse sobre o **Status** célula para uma tarefa com deadlock ou aguardando obter mais informações sobre o bloco. **Aviso:** as **tarefas** janela reporta deadlock apenas uma tarefa bloqueada que usa um primitivo de sincronização que é suportado pela WCT Wait Chain Traversal (). Por exemplo, para um deadlock <xref:System.Threading.Tasks.Task> objeto, que usa WCT, o depurador informa **-com deadlock aguardando**. Para uma tarefa com deadlock que é gerenciada pelo tempo de execução de simultaneidade, que não usa WCT, o depurador informa **esperando**. Para obter mais informações sobre o WCT, consulte [Wait Chain Traversal](/windows/desktop/Debug/wait-chain-traversal).|
|**Hora de início**|A hora em que a tarefa se tornou ativa.|
|**Duração**|O número de segundos que a tarefa esteve ativa.|
|**Tempo de conclusão**|A hora em que a tarefa foi concluída.|
|**Local**|O local atual da pilha de chamadas da tarefa. Passe o mouse sobre esta célula para ver a pilha de chamada inteira para a tarefa. As tarefas agendadas não têm um valor nessa coluna.|
|**Tarefa**|O método inicial e quaisquer argumentos que são passados para a tarefa quando ela foi criada.|
|**AsyncState**|Para código gerenciado, o status da tarefa. Por padrão, essa coluna está ocultada. Para exibir esta coluna, abra o menu de contexto para um dos cabeçalhos de coluna. Escolher **colunas**, **AsyncState**.|
|**Parent**|A ID da tarefa que criou essa tarefa. Se estiver em branco, a tarefa não terá pai. Isso é aplicável somente para programas gerenciados.|
|**Atribuição de thread**|O nome e a ID do thread no qual a tarefa está em execução.|
|**AppDomain**|Para código gerenciado, o domínio de aplicativo no qual a tarefa está em execução.|
|**task_group**|Para código nativo, o endereço do [task_group](/cpp/parallel/concrt/reference/task-group-class) objeto que a tarefa agendada. Para agentes assíncronos e tarefas leves, essa coluna é definida como 0.|
|**Processo**|A ID do processo no qual a tarefa está em execução.|

 Você pode adicionar colunas à exibição clicando com o botão direito em um cabeçalho de coluna e selecionando as colunas desejadas. (Remover colunas desmarcando as seleções.) Você também pode reorganizar as colunas arrastando-as para a esquerda ou direita. O menu de atalho da coluna é mostrado na ilustração a seguir.

 ![Menu de exibição de atalho na janela de tarefas](../debugger/media/parallel_tasks_contextmenu.png "Parallel_Tasks_ContextMenu")

## <a name="sorting-tasks"></a>Tarefas de classificação
 Para classificar as tarefas por critérios da coluna, clique no cabeçalho da coluna. Por exemplo, clicando o **ID** cabeçalho de coluna, você pode classificar as tarefas por ID da tarefa: 1,2,3,4,5 e assim por diante. Para inverter a ordem de classificação, clique no cabeçalho da coluna novamente. A coluna e a ordem de classificação atuais estão indicadas por uma seta na coluna.

## <a name="grouping-tasks"></a>Agrupando tarefas
 Você pode agrupar tarefas com base em qualquer coluna na exibição de lista. Por exemplo, clicando com o **Status** cabeçalho de coluna e, em seguida, clicando em **Group by** > **[*status*]**, você pode Agrupe todas as tarefas que têm o mesmo status. Por exemplo, você pode ver rapidamente esperando tarefas para que você pode se concentrar em por que estão bloqueadas. Você também pode recolher um grupo que não é de interesse durante a sessão de depuração. Da mesma forma, você pode agrupar por outras colunas. Um grupo pode ser sinalizado ou ter a sinalização removida apenas clicando no botão ao lado do cabeçalho do grupo. A ilustração a seguir mostra a **tarefas** janela no modo agrupado.

 ![Modo agrupado na janela de tarefas](../debugger/media/parallel_tasks_groupedmode.png "Parallel_Tasks_GroupedMode")

## <a name="parent-child-view"></a>Exibição de pai-filho
 (Essa exibição está disponível apenas para código gerenciado). Clicando com o **Status** cabeçalho de coluna e, em seguida, clicando em **Group by** > **pai**, você pode alterar a lista de tarefas para uma exibição hierárquica, na qual todas as tarefas filho é um subnó que pode ser exibido ou ocultado em seu pai.

## <a name="flagging-tasks"></a>Tarefas de sinalização
 Você pode sinalizar o thread a tarefa em que uma tarefa está em execução, selecionando a tarefa listar item e, em seguida, escolhendo **sinalizar Thread atribuído** no menu de contexto ou clicando no ícone de sinalizador na primeira coluna. Se você sinalizar várias tarefas, poderá classificar na coluna do sinalizador para levar todas as tarefas sinalizadas para o alto para que você possa se concentrar apenas nelas. Você também pode usar o **pilhas paralelas** janela para exibir apenas tarefas sinalizadas. Isso permite filtrar tarefas nas quais você não está interessado para depuração. Os sinalizadores não são mantidos entre sessões de depuração.

## <a name="freezing-and-thawing-tasks"></a>Congelando e descongelando tarefas
 Você pode congelar o thread no qual uma tarefa está em execução, clicando duas vezes o item de lista de tarefas e, em seguida, clicando em **congelar Thread atribuído**. (Se uma tarefa já está congelada, o comando será **descongelar Thread atribuído**.) Quando você congela um thread, esse thread não será executado quando você percorre o código após o ponto de interrupção atual. O **congelar todos os Threads, mas este um** comando congelará todos os threads, exceto o que está executando o item de lista de tarefas.

 A ilustração a seguir mostra os outros itens de menu para cada tarefa.

 ![Menu de thread de atalho na janela de tarefas](../debugger/media/parallel_tasks_contextmenu2.png "Parallel_Tasks_ContextMenu2")

## <a name="switching-the-active-task-or-frame"></a>Alternando a tarefa ativa ou o quadro

O **alternar para tarefas** comando torna a tarefa atual a tarefa ativa. O **alternar para quadro** comando torna a pilha selecionada de quadro o quadro de pilhas ativas. Alterna o contexto do depurador para a tarefa atual ou o quadro de pilhas selecionado.

## <a name="see-also"></a>Consulte também

- [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
- [Programação paralela](/dotnet/standard/parallel-programming/index)
- [Tempo de Execução de Simultaneidade](/cpp/parallel/concrt/concurrency-runtime)
- [Usando a janela Pilhas Paralelas](../debugger/using-the-parallel-stacks-window.md)
- [Passo a passo: depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)