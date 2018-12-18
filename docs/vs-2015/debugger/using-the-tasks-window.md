---
title: Usando a janela tarefas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.paralleltasks
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: bd5e0612-a0dc-41cf-a7af-1e87d0d5c35f
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa59e1e57750c9c2075c10c76ab5c518ed0e8686
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793894"
---
# <a name="using-the-tasks-window"></a>Usando a janela Tarefas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **tarefas** janela se parece com o **Threads** janela, exceto que mostra informações sobre <xref:System.Threading.Tasks.Task?displayProperty=fullName>, [task_handle](http://msdn.microsoft.com/library/b4af5b28-227d-4488-8194-0a0d039173b7), ou [WinJS. Promise ](http://msdn.microsoft.com/library/windows/apps/br211867.aspx) objetos em vez de cada thread. Como threads, as tarefas representam as operações assíncronas que podem ser executadas simultaneamente; no entanto, várias tarefas podem ser executadas no mesmo thread. Ver [programação assíncrona em JavaScript (aplicativos da Windows Store)](http://msdn.microsoft.com/library/windows/apps/hh700330.aspx) para obter mais informações.  
  
 No código gerenciado, você pode usar o **tarefas** janela quando você trabalha com <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos ou com o **await** e **async** palavras-chave (**Await** e **Async** no Visual Basic). Para obter mais informações sobre as tarefas no código gerenciado, consulte [programação paralela](http://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d).  
  
 No código nativo, você pode usar o **tarefas** janela quando você trabalha com [grupos de tarefas](http://msdn.microsoft.com/library/42f05ac3-2098-494a-ba84-737fcdcad077), [algoritmos em paralelo](http://msdn.microsoft.com/library/045dca7b-4d73-4558-a44c-383b88a28473), [agentes assíncronos](http://msdn.microsoft.com/library/6cf6ccc6-87f1-4e14-af15-ea8ba58fef1a), e [tarefas leves](http://msdn.microsoft.com/library/9aba278c-e0c9-4ede-b7c6-fedf7a365d90). Para obter mais informações sobre as tarefas no código nativo, consulte [tempo de execução de simultaneidade](http://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c).  
  
 No JavaScript, você pode usar a janela Tarefas quando estiver trabalhando com a tarefa e, em seguida, codificar.  
  
 Você pode usar o **tarefas** janela sempre que você invadir o depurador. Você pode acessá-lo na **Debug** menu clicando **Windows** e, em seguida, clicando em **tarefas**. A ilustração a seguir mostra a **tarefas** janela no modo padrão.  
  
 ![Janela tarefas paralelas](../debugger/media/parallel-tasks-window.png "Parallel_Tasks_Window")  
  
> [!NOTE]
>  No código gerenciado, um <xref:System.Threading.Tasks.Task> que tem um status de <xref:System.Threading.Tasks.TaskStatus>, <xref:System.Threading.Tasks.TaskStatus> ou <xref:System.Threading.Tasks.TaskStatus> podem não ser exibidos na janela das tarefas quando os threads gerenciados estão em um estado de suspensão ou junção.  
  
## <a name="tasks-column-information"></a>Informações da coluna de tarefas  
 As colunas na **tarefas** janela Mostrar as informações a seguir.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**sinalizadores**|Mostra quais tarefas estão sinalizadas e permite sinalizar ou remover a sinalização de uma tarefa.|  
|**Ícones**|Uma seta amarela indica a tarefa atual. A tarefa atual é a tarefa mais alta no thread atual.<br /><br /> Uma seta branca indica a tarefa de quebra, isto é, a que era atual quando o depurador foi chamado.<br /><br /> O ícone de pausa indica uma tarefa que foi congelada pelo usuário. Você pode congelar e descongelar uma tarefa clicando com o botão direito na lista.|  
|**ID**|Um número fornecido pelo sistema para a tarefa. No código nativo, esse é o endereço da tarefa.|  
|**Status**|O estado atual (agendado, ativo, com deadlock, aguardando ou concluído) da tarefa. Uma tarefa agendada é aquela que ainda não foi executada e, portanto, ainda não tem uma pilha de chamadas, um thread alocado ou as informações relacionadas.<br /><br /> Uma tarefa ativa é aquela que estava executando o código antes de quebrar no depurador.<br /><br /> Uma tarefa de espera é bloqueada porque está esperando um evento ser sinalizado, um bloqueio ser liberado ou outra tarefa ser concluída.<br /><br /> Uma tarefa com deadlock é uma tarefa de espera cujo thread está bloqueado com outro thread.<br /><br /> Passe o mouse sobre o **Status** célula para uma tarefa com deadlock ou aguardando obter mais informações sobre o bloco. **Aviso:** as **tarefas** janela reporta deadlock apenas uma tarefa bloqueada que usa um primitivo de sincronização que é suportado pela WCT Wait Chain Traversal (). Por exemplo, para um deadlock <xref:System.Threading.Tasks.Task> objeto, que usa WCT, o depurador informa **aguardando-com deadlock**. Para uma tarefa com deadlock que é gerenciada pelo tempo de execução de simultaneidade, que não usa WCT, o depurador informa **esperando**. Para obter mais informações sobre o WCT, consulte [Wait Chain Traversal](http://msdn.microsoft.com/library/ms681622\(VS.85\).aspx).|  
|**Hora de início**|A hora em que a tarefa se tornou ativa.|  
|**Duração**|O número de segundos que a tarefa esteve ativa.|  
|**Tempo de conclusão**|A hora em que a tarefa foi concluída.|  
|**Local**|O local atual da pilha de chamadas da tarefa. Passe o mouse sobre esta célula para ver a pilha de chamada inteira para a tarefa. As tarefas agendadas não têm um valor nessa coluna.|  
|**Tarefa**|O método inicial e quaisquer argumentos que são passados para a tarefa quando ela foi criada.|  
|**Parent**|A ID da tarefa que criou essa tarefa. Se estiver em branco, a tarefa não terá pai. Isso é aplicável somente para programas gerenciados.|  
|**Atribuição de thread**|O nome e a ID do thread no qual a tarefa está em execução.|  
|**Status de retorno**|O status da tarefa quando foi concluída. Os valores de status de retorno são **sucesso**, **cancelado**, e **erro**.|  
|**AppDomain**|Para código gerenciado, o domínio de aplicativo no qual a tarefa está em execução.|  
|**task_group**|Para código nativo, o endereço do [task_group](http://msdn.microsoft.com/library/b4af5b28-227d-4488-8194-0a0d039173b7) objeto que a tarefa agendada. Para agentes assíncronos e tarefas leves, essa coluna é definida como 0.|  
|Processo|A ID do processo no qual a tarefa está em execução.|  
|Estado assíncrono|Para código gerenciado, o status da tarefa. Por padrão, essa coluna está ocultada. Para exibir esta coluna, abra o menu de contexto para um dos cabeçalhos de coluna. Escolher **colunas**, **AsyncState**.|  
  
 Você pode adicionar colunas à exibição clicando com o botão direito em um cabeçalho de coluna e selecionando as colunas desejadas. (Remover colunas desmarcando as seleções.) Você também pode reorganizar as colunas arrastando-as para a esquerda ou direita. O menu de atalho da coluna é mostrado na ilustração a seguir.  
  
 ![Menu de exibição de atalho na janela tarefas paralelas](../debugger/media/parallel-tasks-contextmenu.png "Parallel_Tasks_ContextMenu")  
  
## <a name="sorting-tasks"></a>Tarefas de classificação  
 Para classificar as tarefas por critérios da coluna, clique no cabeçalho da coluna. Por exemplo, clicando o **ID** cabeçalho de coluna, você pode classificar as tarefas por ID da tarefa: 1,2,3,4,5 e assim por diante. Para inverter a ordem de classificação, clique no cabeçalho da coluna novamente. A coluna e a ordem de classificação atuais estão indicadas por uma seta na coluna.  
  
## <a name="grouping-tasks"></a>Agrupando tarefas  
 Você pode agrupar tarefas com base em qualquer coluna na exibição de lista. Por exemplo, clicando com o **Status** cabeçalho de coluna e, em seguida, clicando em **Agrupar por Status**, você pode agrupar todas as tarefas que têm o mesmo status. Por exemplo, você pode visualizar rapidamente as tarefas em espera para que poder se concentrar em por que estão bloqueadas. Você também pode recolher um grupo que não é de interesse durante a sessão de depuração. Da mesma forma, você pode agrupar por outras colunas. Um grupo pode ser sinalizado ou ter a sinalização removida apenas clicando no botão ao lado do cabeçalho do grupo. A ilustração a seguir mostra a **tarefas** janela no modo agrupado.  
  
 ![Modo agrupado na janela tarefas paralelas](../debugger/media/parallel-tasks-groupedmode.png "Parallel_Tasks_GroupedMode")  
  
## <a name="parent-child-view"></a>Exibição de pai-filho  
 (Essa exibição está disponível apenas para código gerenciado). Clicando duas vezes um título de coluna e, em seguida, clicando em **exibição de pai-filho**, você pode alterar a lista de tarefas para uma exibição hierárquica, na qual cada filho a tarefa é um subnó que pode ser exibido ou ocultado em seu pai. A ilustração a seguir mostra as tarefas na exibição de pai-filho.  
  
 ![Pai&#45;exibição-filho na janela tarefas paralelas](../debugger/media/parallel-tasks-parentchildview.png "Parallel_Tasks_ParentChildView")  
  
## <a name="flagging-tasks"></a>Tarefas de sinalização  
 Você pode sinalizar o thread a tarefa em que uma tarefa está em execução, selecionando a tarefa listar item e, em seguida, escolhendo **sinalizador** no menu de contexto ou clicando no ícone de sinalizador na primeira coluna. Se você sinalizar várias tarefas, poderá classificar na coluna do sinalizador para levar todas as tarefas sinalizadas para o alto para que você possa se concentrar apenas nelas. Você também pode usar o **pilhas paralelas** janela para exibir apenas tarefas sinalizadas. Isso permite filtrar tarefas nas quais você não está interessado para depuração. Os sinalizadores não são mantidos entre sessões de depuração.  
  
## <a name="freezing-and-thawing-tasks"></a>Congelando e descongelando tarefas  
 Você pode congelar o thread no qual uma tarefa está em execução, clicando duas vezes o item de lista de tarefas e, em seguida, clicando em **congelar Thread atribuído**. (Se uma tarefa já está congelada, o comando será **descongelar Thread atribuído**.) Quando você congela um thread, esse thread não será executado quando você percorre o código após o ponto de interrupção atual. O **congelar todos os Threads exceto esse** comando congelará todos os threads, exceto o que está executando o item de lista de tarefas.  
  
 A ilustração a seguir mostra os outros itens de menu para cada tarefa.  
  
 ![Menu de thread de atalho na janela tarefas paralelas](../debugger/media/parallel-tasks-contextmenu2.png "Parallel_Tasks_ContextMenu2")  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas do depurador](../debugger/debugger-basics.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Programação paralela](http://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)   
 [Tempo de execução de simultaneidade](http://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)   
 [Usando a janela pilhas paralelas](../debugger/using-the-parallel-stacks-window.md)   
 [Passo a passo: depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)



