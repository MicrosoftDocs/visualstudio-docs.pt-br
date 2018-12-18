---
title: Exibição Threads (desempenho paralelo) | Microsoft Docs
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
- vs.performance.view.threadblocking
helpviewer_keywords:
- Concurrency Visualizer, Threads View (Parallel Performance)
ms.assetid: 2e441103-a266-407b-88c3-fb58716257a3
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 39457684ba19ecbb0ad2ef82caa349e67cdaf8a7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756331"
---
# <a name="threads-view-parallel-performance"></a>Exibição de threads (desempenho em paralelo)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A Exibição Threads é a exibição mais detalhada e com uma grande variedade de recursos da Visualização Simultânea. Ao usar essa exibição, é possível identificar se os threads estão sendo executados ou bloqueados devido à sincronização, E/S ou a algum outro motivo.  
  
 Durante a análise do perfil, a Visualização Simultânea examina todos os eventos de alternância de contexto do sistema operacional em cada thread do aplicativo. Alternâncias de contexto podem ocorrer por vários motivos, como estes:  
  
- Um thread é bloqueado em um primitivo de sincronização.  
  
- O quantum de um thread expira.  
  
- Um thread faz uma solicitação de E/S de bloqueio.  
  
  A Exibição Threads atribui uma categoria a cada alternância de contexto quando um thread interrompe a execução. As categorias são mostradas na legenda, na parte inferior esquerda da exibição. A Visualização Simultânea categoriza eventos de alternância de contexto pesquisando APIs de bloqueio conhecidas na pilha de chamadas do thread. Se não houver nenhuma correspondência de pilha de chamadas, o motivo de espera fornecido por [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] será usado. No entanto, a categoria [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] pode se basear em um detalhe de implementação e pode não refletir a intenção do usuário. Por exemplo, [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] relata o motivo de espera do bloqueio em um bloqueio de leitor-gravador compacto nativo como E/S em vez de sincronização. Na maioria dos casos, é possível identificar a causa raiz de um evento de bloqueio examinando as pilhas de chamadas que correspondem aos eventos de alternância de contexto.  
  
  A Exibição Threads também mostra as dependências entre threads. Por exemplo, se você identificar um thread que está bloqueado em um objeto de sincronização, será possível procurar o thread que o desbloqueou e examinar a atividade na pilha de chamadas desse thread no ponto em que ele desbloqueou o outro.  
  
  Quando os threads estão em execução, a Visualização Simultânea coleta amostras. Na Exibição Threads, é possível analisar qual código é executado por um ou mais threads durante um segmento de execução. Você também pode examinar os relatórios de bloqueio e os relatórios que criam o perfil da execução da árvore de pilha de chamadas.  
  
## <a name="usage"></a>Uso  
 Estas são algumas maneiras pelas quais é possível usar a Exibição Threads:  
  
-   Identifique os motivos pelos quais a interface do usuário de um aplicativo não responde durante determinadas fases de execução.  
  
-   Identifique a quantidade de tempo gasto no bloqueio em sincronização, E/S, falhas de página e em outros eventos.  
  
-   Identifique o grau de interferência de outros processos que estão em execução no sistema.  
  
-   Identifique problemas de balanceamento de carga na execução paralela.  
  
-   Identifique os motivos de escalabilidade que é inexistente ou que está abaixo do ideal (por exemplo, por que o desempenho de um aplicativo paralelo não melhora quando mais núcleos lógicos estão disponíveis).  
  
-   Entenda o grau de simultaneidade no aplicativo, para ajudar na paralelização.  
  
-   Entenda as dependências entre os threads de trabalho e os caminhos críticos de execução.  
  
## <a name="examining-specific-time-intervals-and-threads"></a>Examinando threads e intervalos de tempo específicos  
 A Exibição Threads mostra uma linha do tempo. É possível aplicar zoom e panorâmica à linha do tempo para examinar intervalos e threads específicos do aplicativo. No eixo X é mostrado o tempo e no eixo Y são mostrados vários canais:  
  
- Dois canais de E/S para cada unidade de disco do sistema, um canal para leituras e outro para gravações.  
  
- Um canal para cada thread no processo.  
  
- Canais de marcador, se houver eventos de marcador no rastreamento. Inicialmente, os canais de marcador são exibidos sob os canais de thread que geraram esses eventos.  
  
- Canais de GPU.  
  
  Esta é uma ilustração da Exibição de Threads:  
  
  ![Exibição de threads](../profiling/media/threadsviewnarrowing.png "ThreadsViewNarrowing")  
  Modo de Exibição de Threads  
  
  Inicialmente, os threads são classificados na ordem em que são criados, para que o thread do aplicativo principal seja o primeiro. É possível usar a opção de classificação no canto superior esquerdo da exibição para classificar threads por outro critério (por exemplo, pela maioria dos trabalhos de execução executada).  
  
  É possível ocultar threads que não estão executando o trabalho selecionando seus nomes na coluna à esquerda e, em seguida, escolhendo o botão **Ocultar Threads Selecionados** na barra de ferramentas. Recomendamos ocultar os threads completamente bloqueados, pois suas estatísticas são irrelevantes e podem obstruir os relatórios.  
  
  Para identificar threads adicionais a serem ocultados, na legenda ativa, escolha o relatório **Resumo Por Thread** na guia **Relatório de Perfil**. Isso exibe o gráfico de Detalhamento da Execução, que mostra o estado de threads para o intervalo de tempo selecionado. Em alguns níveis de zoom, alguns threads podem não ser exibidos. Quando isso ocorre, elipses são exibidas à direita.  
  
  Depois de selecionar um intervalo de tempo e alguns threads nele, é possível iniciar a análise de desempenho.  
  
## <a name="analysis-tools"></a>Ferramentas de análise  
 Esta seção descreve os relatórios e outras ferramentas de análise.  
  
### <a name="thread-blocking-details"></a>Detalhes de bloqueio de thread  
 Para obter informações sobre um evento de bloqueio em uma região específica de um thread, coloque o ponteiro na região para exibir uma dica de ferramenta. Ele contém informações como categoria, hora de início da região, duração de bloqueio e uma API de bloqueio, se houver. Se você selecionar a região de bloqueio, a pilha nesse ponto no tempo será exibida no painel inferior, junto com as mesmas informações exibidas na dica de ferramenta. Ao examinar a pilha de chamadas, é possível determinar o motivo subjacente para o evento de bloqueio de thread. É possível encontrar mais informações sobre o processo e o thread selecionando o segmento e examinando a guia Atual.  
  
 Um caminho de execução pode ter vários eventos de bloqueio. É possível examiná-los por categoria de bloqueio, para que você possa encontrar áreas com problemas mais rapidamente. Basta escolher uma das categorias de bloqueio na legenda à esquerda.  
  
### <a name="dependencies-between-threads"></a>Dependências entre threads  
 A Visualização Simultânea pode mostrar as dependências entre os threads no processo, para que você possa determinar o que um thread bloqueado estava tentando fazer e saber qual outro thread habilitou sua execução. Para determinar qual thread desbloqueou outro thread, selecione o segmento de bloqueio relevante. Se a Visualização Simultânea conseguir determinar o thread de desbloqueio, ela desenhará uma linha entre o thread de desbloqueio e o segmento de execução que segue o segmento de bloqueio. Além disso, a guia **Desbloqueando pilha** mostra a pilha de chamadas relevante.  
  
### <a name="thread-execution-details"></a>Detalhes de execução de thread  
 No gráfico de linha do tempo de um thread, os segmentos verdes mostram quando ele estava executando o código. É possível obter informações mais detalhadas sobre um segmento de execução.  
  
 Ao selecionar um ponto em um segmento de execução, a Visualização Simultânea procura esse ponto no tempo na pilha de chamadas relevante e, em seguida, exibe um cursor preto acima do ponto selecionado no segmento de execução e exibe a própria pilha de chamadas na guia **Pilha atual**. É possível selecionar vários pontos no segmento de execução.  
  
> [!NOTE]
>  A Visualização Simultânea pode não conseguir resolver uma seleção em um segmento de execução. Normalmente, isso ocorre quando a duração do segmento é inferior a um milissegundo.  
  
 Para obter um perfil de execução para todos os threads habilitados (não ocultos) no intervalo de tempo selecionado, escolha o botão **Execução** na legenda ativa.  
  
### <a name="timeline-graph"></a>Gráfico de linha do tempo  
 O gráfico de linha do tempo mostra a atividade de todos os threads no processo e todos os dispositivos de disco físico no computador host. Ele também exibe a atividade da GPU e eventos de marcador.  É possível ampliar para exibir mais detalhes ou reduzir para exibir um intervalo de tempo mais longo. Você também pode selecionar pontos no gráfico para obter detalhes sobre categorias, horas de início, durações e estados da pilha de chamadas.  
  
 No gráfico de linha do tempo, uma cor indica o estado de um thread em determinado momento. Por exemplo, segmentos verdes estavam sendo executados, segmentos vermelhos foram bloqueados para sincronização, segmentos amarelos foram impedidos e segmentos roxos foram usados na E/S do dispositivo. É possível usar essa exibição para examinar o equilíbrio de trabalho entre os threads envolvidos em um loop paralelo ou em tarefas simultâneas. Se um thread estiver levando mais tempo para ser concluído do que os outros, o trabalho poderá estar desbalanceado. É possível usar essas informações para melhorar o desempenho do programa distribuindo o trabalho de modo mais uniforme entre os threads.  
  
 Se apenas um thread estiver verde (em execução) em um ponto no tempo, o aplicativo poderá não estar aproveitando ao máximo a simultaneidade no sistema. É possível usar o gráfico de linha do tempo para examinar as dependências entre os threads e os relacionamentos temporais entre os threads de bloqueio e bloqueados. Para reorganizar os threads, selecione um thread e, na barra de ferramentas, escolha o botão superior ou inferior. Para ocultar threads, selecione-os e escolha o botão **Ocultar Threads**.  
  
### <a name="profile-reports"></a>Relatórios de perfil  
 Abaixo do gráfico de linha do tempo há um perfil de linha do tempo e um painel que contém guias para vários relatórios. Os relatórios são atualizados automaticamente quando você muda a Exibição Threads. Para rastreamentos grandes, o painel de relatórios pode ficar indisponível quando as atualizações são calculadas. Cada relatório tem dois ajustes de filtro: redução de ruído e Apenas Meu Código. Use a redução de ruído para filtrar as entradas da árvore de chamadas nos casos em que pouco tempo é gasto. O valor de filtro padrão é 2%, mas é possível ajustá-lo de 0% a 99%. Para exibir somente a árvore de chamadas do código, marque a caixa de seleção **Apenas Meu Código**. Para exibir todas as árvores de chamadas, desmarque essa caixa de seleção.  
  
#### <a name="profile-report"></a>Relatório de perfil  
 Esta guia mostra relatórios que correspondem às entradas na legenda ativa. Para exibir um relatório, escolha uma das entradas.  
  
#### <a name="current-stack"></a>Pilha atual  
 Esta guia mostra a pilha de chamadas de um ponto selecionado em um segmento de thread no gráfico de linha do tempo. As pilhas de chamadas são cortadas para mostrar somente a atividade que está relacionada ao programa.  
  
#### <a name="unblocking-stack"></a>Desbloqueando pilha  
 Para ver qual thread desbloqueou o thread selecionado e em qual linha de código, escolha a guia **Desbloqueando pilha**.  
  
#### <a name="execution"></a>Execução  
 O Relatório de Execução mostra o detalhamento do tempo gasto pelo aplicativo na execução.  
  
 Para localizar a linha de código em que o tempo de execução é gasto, expanda a árvore de chamadas e, no menu de atalho da entrada da árvore de chamadas, escolha **Exibir Fonte** ou **Exibir Sites de Chamada**. **Exibir Fonte** localiza a linha de código executada. **Exibir Sites de Chamada** localiza a linha de código que chamou a linha de código executada. Se houver apenas um único site de chamada, a linha de código será realçada. Se existirem vários sites de chamada, você poderá selecionar o site desejado na caixa de diálogo exibida e, em seguida, escolher o botão **Ir para fonte** para realçar o código do site de chamada. Geralmente, é mais útil localizar o site de chamada que tem a maioria das instâncias, mais tempo ou ambos. Para obter mais informações, consulte [Relatório de perfil de execução](../profiling/execution-profile-report.md).  
  
#### <a name="synchronization"></a>Sincronização  
 O relatório de sincronização mostra as chamadas responsáveis por blocos de sincronização, junto com os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de sincronização](../profiling/synchronization-time.md).  
  
#### <a name="io"></a>E/S  
 O relatório de E/S mostra as chamadas responsáveis por blocos de E/S, junto com os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de E/S (Exibição Threads)](../profiling/i-o-time-threads-view.md).  
  
#### <a name="sleep"></a>Sleep  
 O relatório de suspensão mostra as chamadas responsáveis por blocos de suspensão, junto com os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de suspensão](../profiling/sleep-time.md).  
  
#### <a name="memory-management"></a>Gerenciamento de memória  
 O relatório de gerenciamento de memória mostra as chamadas em que ocorreram blocos de gerenciamento de memória, junto com os tempo de bloqueio agregados de cada pilha de chamadas. É possível usar essas informações para identificar as áreas que apresentam problemas de coleta de lixo ou de paginação em excesso.  Para obter mais informações, consulte [Tempo de gerenciamento de memória](../profiling/memory-management-time.md).  
  
#### <a name="preemption"></a>Preempção  
 O relatório de Preempção mostra as instâncias em que os processos do sistema impediram o processo atual e os threads individuais que substituíram os threads no processo atual. É possível usar essas informações para identificar os processos e os threads que são mais responsáveis pela preempção. Para obter mais informações, consulte [Tempo de preempção](../profiling/preemption-time.md).  
  
#### <a name="ui-processing"></a>Processamento de interface do usuário  
 O relatório de processamento de interface do usuário mostra as chamadas responsáveis por blocos de processamento de interface do usuário, junto com os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de processamento de interface do usuário](../profiling/ui-processing-time.md).  
  
#### <a name="per-thread-summary"></a>Por Resumo de Thread  
 Esta guia mostra uma exibição de coluna codificada por cores do tempo total gasto por cada thread no estado de execução, bloqueio, E/S e outros estados. As colunas são rotuladas na parte inferior. Ao ajustar o nível de zoom no gráfico de linha do tempo, essa guia é atualizada automaticamente. Em alguns níveis de zoom, alguns threads podem não ser exibidos. Quando isso ocorre, elipses são exibidas à direita. Se o thread desejado não for exibido, será possível ocultar outros threads. Para obter mais informações, consulte [Relatório de resumo por thread](../profiling/per-thread-summary-report.md).  
  
#### <a name="disk-operations"></a>Operações de disco  
 Esta guia mostra quais processos e threads estavam envolvidos na E/S de disco em nome do processo atual, quais arquivos foram cobertos (por exemplo, DLLs carregadas), quantos bytes foram lidos e outras informações. É possível usar esse relatório para avaliar o tempo gasto no acesso a arquivos durante a execução, especialmente quando o processo parece estar associado à E/S. Para obter mais informações, consulte [Relatório de operações de disco](../profiling/disk-operations-report-threads-view.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visualização Simultânea](../profiling/concurrency-visualizer.md)



