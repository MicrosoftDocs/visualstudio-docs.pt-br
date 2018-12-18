---
title: Exibição Threads na Visualização Simultânea | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.threadblocking
helpviewer_keywords:
- Concurrency Visualizer, Threads View (Parallel Performance)
ms.assetid: 2e441103-a266-407b-88c3-fb58716257a3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ce7cf5cf0534a0e989b65d6e67451fe2a7c496ab
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388899"
---
# <a name="threads-view-in-the-concurrency-visualizer"></a>Exibição Threads na Visualização Simultânea

A exibição **Threads** é a exibição mais detalhada e repleta de funcionalidades da Visualização Simultânea. Na exibição **Threads**, você pode identificar quais threads estão executando um código durante um segmento de execução e analisar se os threads estão sendo executados ou bloqueados devido à sincronização, à E/S ou a outros motivos. Os relatórios da exibição **Threads** também analisam threads de desbloqueio e de execução da árvore de pilha de chamadas.

Enquanto os threads estão em execução, a Visualização Simultânea coleta amostras. Quando um thread interrompe a execução, o visualizador examina todos os eventos de alternância de contexto do sistema operacional para o thread. As alternâncias de contexto podem ocorrer porque:  
  
- Um thread é bloqueado em um primitivo de sincronização.  
- O quantum de um thread expira.  
- Um thread faz uma solicitação de E/S de bloqueio.  

A Visualização Simultânea categoriza eventos de thread e de alternância de contexto e pesquisa APIs de bloqueio conhecidas nas pilhas de chamadas de threads. Ela exibe as categorias de thread na legenda ativa no canto inferior esquerdo da exibição **Threads**. Na maioria dos casos, é possível identificar a causa raiz de um evento de bloqueio examinando as pilhas de chamadas que correspondem aos eventos de alternância de contexto.

Se não há nenhuma correspondência de pilha de chamadas, a Visualização Simultânea usa o motivo de espera fornecido pelo [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)]. No entanto, a categoria [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)] pode se basear em um detalhe de implementação e pode não refletir a intenção do usuário. Por exemplo, [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)] relata o motivo de espera do bloqueio em um bloqueio de leitor-gravador compacto nativo como E/S em vez de Sincronização.  
  
A exibição **Threads** também mostra as dependências entre threads. Por exemplo, se você identifica um thread que está bloqueado em um objeto de sincronização, pode encontrar o thread que o desbloqueou. Você pode examinar o thread de desbloqueio na pilha de chamadas no ponto em que ele desbloqueou o outro.  

Use a exibição **Threads** para:  

- Identificar os motivos pelos quais a interface do usuário de um aplicativo não responde durante determinadas fases de execução.  
- Determinar o tempo gasto no bloqueio em sincronização, em E/S, em falhas de página e em outros eventos.  
- Descobrir o grau de interferência de outros processos em execução no sistema.  
- Identifique problemas de balanceamento de carga na execução paralela.  
- Encontrar os motivos de escalabilidade abaixo do ideal ou inexistente. Por exemplo, por que o desempenho de um aplicativo paralelo não melhora quando mais núcleos lógicos estão disponíveis.  
- Entenda o grau de simultaneidade no aplicativo, para ajudar na paralelização.  
- Identificar as dependências entre os threads de trabalho e os caminhos críticos de execução.  
  
## <a name="use-threads-view"></a>Usar a exibição Threads 

Para iniciar a Visualização Simultânea, selecione **Analisar** > **Visualização Simultânea** e, em seguida, selecione uma opção, como **Iniciar Novo Processo**. 

A Visualização Simultânea inicia o aplicativo e coleta um rastreamento até que você selecione **Parar Coleta**. Em seguida, o visualizador analisa o rastreamento e exibe os resultados na página do relatório de rastreamento. 

Selecione a guia **Threads** no canto superior esquerdo do relatório para abrir a exibição **Threads**. 

![Exibição Threads](../profiling/media/threadsviewnarrowing.png "Threads view")  
  
Selecione intervalos de tempo e threads para iniciar uma análise de desempenho.  
  
## <a name="timeline-analysis"></a>Análise da linha do tempo  

A parte superior da exibição **Threads** é uma linha do tempo. A linha do tempo mostra a atividade de todos os threads no processo e todos os dispositivos de disco físico no computador host. Ele também exibe a atividade da GPU e eventos de marcador.  

Na linha do tempo, o eixo X é o tempo e no eixo Y estão vários canais:  
  
- Dois canais de E/S para cada unidade de disco do sistema, um canal para leituras e outro para gravações.  
- Um canal para cada thread no processo.  
- Canais de marcador, se houver eventos de marcador no rastreamento. Inicialmente, os canais de marcador são exibidos sob os canais de thread que geraram esses eventos.  
- Canais de GPU.  
  
Inicialmente, os threads são classificados na ordem em que são criados, de modo que o thread do aplicativo principal seja o primeiro. Selecione outra opção na lista suspensa **Classificar por** para classificar threads por outro critério, como **Execução**. 

As cores na linha do tempo indicam o estado de um thread em determinado momento. Os segmentos verdes estão em execução, os segmentos vermelhos estão bloqueados para sincronização, os segmentos amarelos foram impedidos e os segmentos roxos são usados na E/S do dispositivo. 

Amplie para exibir mais detalhes ou reduza para exibir um intervalo de tempo mais longo. Selecione segmentos e pontos no grafo para obter detalhes sobre categorias, horas de início, atrasos e estados da pilha de chamadas.  

Use a linha do tempo para examinar o equilíbrio de trabalho entre os threads envolvidos em um loop paralelo ou em tarefas simultâneas. Se um thread estiver levando mais tempo para ser concluído do que os outros, o trabalho poderá estar desbalanceado. Melhore o desempenho do aplicativo distribuindo o trabalho de maneira mais uniforme entre os threads.  
  
Se apenas um thread estiver em execução em um ponto no tempo, o aplicativo poderá não estar aproveitando ao máximo a simultaneidade no sistema. É possível usar o grafo de linha do tempo para examinar as dependências entre os threads e os relacionamentos temporais entre os threads de bloqueio e bloqueados. Para reorganizar os threads, selecione um thread e, em seguida, selecione o ícone superior ou inferior na barra de ferramentas. 

Oculte os threads que não estão realizando nenhum trabalho ou que estão completamente bloqueados, pois suas estatísticas são irrelevantes e podem obstruir os relatórios. Oculte threads selecionando seus nomes e, em seguida, selecionando o ícones **Ocultar threads selecionados** ou **Ocultar todos os threads, exceto os selecionados** na barra de ferramentas. Para identificar os threads a serem ocultados, selecione o link **Resumo por Thread** no canto inferior esquerdo. Você pode ocultar os threads que não têm nenhuma atividade no grafo **Resumo por Thread**. 

### <a name="thread-execution-details"></a>Detalhes de execução de thread  
Para obter informações mais detalhadas sobre um segmento de execução, selecione um ponto em um segmento verde da linha do tempo. A Visualização Simultânea exibe um cursor preto acima do ponto selecionado e mostra a pilha de chamadas na guia **Atual** do painel inferior. É possível selecionar vários pontos no segmento de execução.  
  
>[!NOTE]
>A Visualização Simultânea pode não conseguir resolver uma seleção em um segmento de execução se a duração do segmento é inferior a um milissegundo.  
  
Para obter um perfil de execução de todos os threads não ocultos no intervalo de tempo atualmente selecionado, selecione **Execução** na legenda no canto inferior esquerdo.  
  
### <a name="thread-blocking-details"></a>Detalhes de bloqueio de thread  
Para obter informações sobre uma região específica em um thread, focalize a região na linha do tempo para exibir uma dica de ferramenta. A dica de ferramenta traz informações como categoria, hora de início e atraso. Selecione a região para exibir a pilha de chamadas nesse ponto no tempo na guia **Atual** do painel inferior. O painel também mostra a categoria, o atraso, a API de bloqueio, se houver uma, bem como o thread de desbloqueio, se houver um. Examinando a pilha de chamadas, você pode determinar os motivos subjacentes dos eventos de bloqueio de thread.  
  
Um caminho de execução pode ter vários eventos de bloqueio. Para examiná-los por categoria de bloqueio e encontrar áreas com problemas mais rapidamente, selecione uma categoria de bloqueio na legenda à esquerda.  
  
### <a name="dependencies-between-threads"></a>Dependências entre threads  
A Visualização Simultânea mostra as dependências entre os threads, para que você possa determinar o que um thread bloqueado estava tentando fazer e qual outro thread habilitou sua execução. 

Para determinar qual thread desbloqueou outro thread, selecione o segmento de bloqueio na linha do tempo. Se a Visualização Simultânea conseguir determinar o thread de desbloqueio, ela desenhará uma linha entre o thread de desbloqueio e o segmento de execução que segue o segmento de bloqueio. Selecione a guia **Pilha de Desbloqueio** no painel inferior para ver a pilha de chamadas relevante.  
  
## <a name="profile-reports"></a>Relatórios de perfil 
Abaixo do grafo de linha do tempo há um painel com as guias de relatório **Relatório de Perfil**, **Atual** e **Pilha de Desbloqueio**. Os relatórios são atualizados automaticamente quando você altera as seleções de linha do tempo e threads. Para rastreamentos grandes, o painel de relatórios pode ficar não disponível temporariamente enquanto as atualizações são calculadas. 

### <a name="profile-report-tab"></a>Guia Relatório de Perfil 

O **Relatório de Perfil** tem dois filtros:

- Para filtrar as entradas da árvore de chamadas nas quais pouco tempo foi gasto, digite um valor de filtro entre 0 e 99% no campo **Redução de ruído no**. O valor padrão é 2%. 
- Para exibir as árvores de chamadas apenas de seu código, marque a caixa de seleção **Apenas Meu Código**. Para exibir todas as árvores de chamadas, desmarque a caixa de seleção.  

A guia **Relatório de Perfil** mostra relatórios para as categorias e os links na legenda. Para exibir um relatório, selecione uma das entradas à esquerda:  

- **Execução**  
  O relatório **Execução** mostra o detalhamento do tempo gasto pelo aplicativo na execução.  
  
  Para encontrar a linha de código em que o tempo de execução é gasto, expanda a árvore de chamadas e, no menu de atalho da entrada da árvore de chamadas, selecione **Exibir Fonte** ou **Exibir Sites de Chamada**. **Exibir Fonte** localiza a linha de código executada. **Exibir Sites de Chamada** localiza a linha de código que chamou a linha executada. Se houver apenas uma única linha de site de chamada, o código será realçado. Se houver vários sites de chamada, selecione aquele desejado na caixa de diálogo e, em seguida, selecione **Ir para fonte**. Geralmente, é mais útil localizar o site de chamada que tem a maioria das instâncias, mais tempo ou ambos. Para obter mais informações, confira [Relatório de perfil de execução](../profiling/execution-profile-report.md).  
  
- **Sincronização**  
  O relatório **Sincronização** mostra as chamadas responsáveis por blocos de sincronização, junto com os tempos de bloqueio totais de cada pilha de chamadas. Para obter mais informações, confira [Tempo de sincronização](../profiling/synchronization-time.md).  
  
- **E/S**  
  O relatório **E/S** mostra as chamadas responsáveis por blocos de E/S, junto com os tempos de bloqueio totais de cada pilha de chamadas. Para obter mais informações, confira [Tempo de E/S (exibição Threads)](../profiling/i-o-time-threads-view.md).  
  
- **Sleep**  
  O relatório **Suspensão** mostra as chamadas responsáveis por blocos de suspensão, junto com os tempos de bloqueio totais de cada pilha de chamadas. Para saber mais, confira [Tempo de suspensão](../profiling/sleep-time.md).  
  
- **Gerenciamento de memória**  
  O relatório **Gerenciamento de Memória** mostra as chamadas em que ocorreram blocos de gerenciamento de memória, junto com os tempos de bloqueio totais de cada pilha de chamadas. Use essas informações para identificar as áreas que apresentam problemas de coleta de lixo ou de paginação em excesso.  Para saber mais, confira [Tempo de gerenciamento de memória](../profiling/memory-management-time.md).  
  
- **Preempção**  
  O relatório **Preempção** mostra em que momentos os processos do sistema impediram o processo atual, bem como os threads individuais que substituíram os threads no processo atual. É possível usar essas informações para identificar os processos e os threads que são mais responsáveis pela preempção. Para saber mais, confira [Tempo de preempção](../profiling/preemption-time.md).  
  
- **Processamento de interface do usuário**  
  O relatório **Processamento de interface do usuário** mostra as chamadas responsáveis por blocos de processamento de interface do usuário, junto com os tempos de bloqueio totais de cada pilha de chamadas. Para saber mais, confira [Tempo de processamento de interface do usuário](../profiling/ui-processing-time.md).  
  
- **Resumo por Thread**  
  Selecione **Resumo por Thread** para exibir um grafo que mostra o estado de threads para o intervalo de tempo atualmente selecionado. As colunas codificadas por cores mostram o tempo total gasto por cada thread nos estados de execução, bloqueio, E/S e outros. Os threads são rotulados na parte inferior. Quando você ajusta o nível de zoom no grafo de linha do tempo, esse grafo é atualizado automaticamente. 
  
  Em alguns níveis de zoom, alguns threads podem não ser mostrados no grafo. Quando isso acontece, são exibidas reticências (**...**) à direita. Se o thread desejado não for exibido, será possível ocultar outros threads. Para obter mais informações, confira [Relatório de resumo por thread](../profiling/per-thread-summary-report.md).  
  
- **Operações de Disco**  
  Selecione **Operações de Disco** para mostrar os processos e os threads envolvidos na E/S de disco do processo atual, os arquivos cobertos (por exemplo, as DLLs carregadas por eles), o número de bytes lidos e outras informações. Use esse relatório para avaliar o tempo gasto no acesso a arquivos durante a execução, especialmente quando o processo parece estar associado à E/S. Para obter mais informações, confira [Relatório de operações de disco](../profiling/disk-operations-report-threads-view.md).  
  
### <a name="current-tab"></a>Guia atual  
Esta guia mostra a pilha de chamadas de um ponto selecionado em um segmento de thread no gráfico de linha do tempo. As pilhas de chamadas são cortadas para mostrar somente a atividade que está relacionada ao aplicativo.  
  
### <a name="unblocking-stack-tab"></a>Guia Pilha de Desbloqueio 
Esta guia mostra qual thread desbloqueou o thread selecionado e a pilha de chamadas de desbloqueio.  
  
## <a name="see-also"></a>Consulte também  
 [Visualização Simultânea](../profiling/concurrency-visualizer.md)
