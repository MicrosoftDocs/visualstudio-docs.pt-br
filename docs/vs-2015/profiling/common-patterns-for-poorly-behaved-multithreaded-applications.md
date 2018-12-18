---
title: Padrões comuns para aplicativos multithread de mau comportamento | Microsoft Docs
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
- vs.cv.threads.tools.gallery
helpviewer_keywords:
- Concurrency Visualizer, common patterns for poorly-behaved multithreaded applications
ms.assetid: 00d10629-e20f-4d6d-8643-c59a3879812e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1e0dfcb9408c67acc754f687903b4be2d13f9ff4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755813"
---
# <a name="common-patterns-for-poorly-behaved-multithreaded-applications"></a>Padrões comuns para aplicativos multithread de mau comportamento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A Visualização Simultânea ajuda os desenvolvedores a visualizarem o comportamento de um aplicativo multithread. Essa ferramenta inclui uma galeria de padrões comuns para aplicativos multithread com mau comportamento. A galeria inclui padrões visual comuns e reconhecíveis expostos por meio da ferramenta, juntamente com uma explicação do comportamento representado por cada padrão, o resultado provável desse comportamento e a abordagem mais comum para resolvê-lo.  
  
## <a name="lock-contention-and-serialized-execution"></a>Contenção de bloqueio e execução serializada  
 ![Contenção de bloqueio que resulta em execução serializada](../profiling/media/lockcontention-serialized.png "LockContention_Serialized")  
  
 Às vezes, um aplicativo paralelizado continua sendo executado em série mesmo que ele tenha vários threads e que o computador tenha um número suficiente de núcleos lógicos. O primeiro sintoma é baixo desempenho multithread, talvez até mesmo um pouco mais lento do que uma implementação serial. No Modo de Exibição de Threads, você não vê vários threads sendo executados em paralelo; em vez disso, você vê que apenas um thread está sendo executado a qualquer momento. Nesse ponto, se você clicar em um segmento de sincronização em um thread, será possível ver uma pilha de chamadas para o thread bloqueado (pilha de chamadas de bloqueio) e o thread que removeu a condição de bloqueio (pilha de chamadas de desbloqueio). Além disso, se a pilha de chamadas de desbloqueio ocorrer no processo que você está analisando, um conector Preparado para Thread será exibido. A partir desse ponto, é possível navegar em seu código nas pilhas de chamadas de bloqueio e desbloqueio para investigar ainda mais a causa da serialização.  
  
 Conforme mostrado na ilustração a seguir, a Visualização Simultânea também pode expor esse sintoma no Modo de Exibição de Utilização da CPU, em que, mesmo na presença de vários threads, o aplicativo consome apenas um núcleo lógico.  
  
 Para obter mais informações, consulte "Performance Pattern 1: Identifying Lock Contention (Padrão de desempenho 1: identificando a contenção de bloqueio)" no blog de Hazim Shafi [Parallel Performance Tools For Windows (Ferramentas de desempenho paralelo para Windows)](http://go.microsoft.com/fwlink/?LinkID=160569) no site da Web do blog do MSDN.  
  
 ![Contenção de bloqueio](../profiling/media/lockcontention-2.png "LockContention_2")  
  
## <a name="uneven-workload-distribution"></a>Distribuição de carga de trabalho não uniforme  
 ![Carga de trabalho não uniforme](../profiling/media/unevenworkload-1.png "UnevenWorkLoad_1")  
  
 Quando ocorre uma distribuição irregular de trabalho entre vários threads paralelos em um aplicativo, um padrão típico de serrilha é exibido à medida que cada thread conclui seu trabalho, conforme mostrado na ilustração anterior. A Visualização Simultânea geralmente mostra horários de início muito perto de cada thread simultâneo. No entanto, esses threads normalmente terminam de maneira irregular em vez de terminar simultaneamente. Esse padrão indica uma distribuição irregular de trabalho entre um grupo de threads paralelos, o que pode levar à redução do desempenho. A melhor abordagem para esse problema é reavaliar o algoritmo pelo qual o trabalho foi dividido entre os threads paralelos.  
  
 Conforme mostrado na ilustração a seguir, a Visualização Simultânea também pode expor esse sintoma no Modo de Exibição de Utilização da CPU como um uma etapa decrescente gradual na utilização da CPU.  
  
 ![Carga de trabalho não uniforme](../profiling/media/unevenworkload-2.png "UnevenWorkload_2")  
  
## <a name="oversubscription"></a>Excesso de assinatura  
 ![Excesso de assinatura](../profiling/media/oversubscription.png "Excesso de assinatura")  
  
 No caso do excesso de assinatura, o número de threads ativos em um processo é maior que o número de núcleos lógicos disponíveis no sistema. A ilustração anterior mostra os resultados do excesso de assinatura, com faixas de preempção significativa em todos os threads ativos. Além disso, a legenda mostra que uma grande percentual de tempo é gasta em preempção (84 por cento neste exemplo). Isso pode indicar que o processo está solicitando que o sistema execute mais threads simultâneos do que o número de núcleos lógicos. No entanto, isso também pode indicar que outros processos no sistema estão usando recursos que deveriam estar disponíveis para esse processo.  
  
 Você deve considerar o seguinte ao avaliar esse problema:  
  
-   O sistema geral pode ter excesso de assinatura. Considere que outros processos no sistema talvez estejam admitindo preempção dos seus threads. Quando você pausa um segmento de preempção no modo de exibição de threads, uma dica de ferramenta identificará o thread e o processo que admitiu preempção do thread. Esse processo não é necessariamente o que foi executado durante o todo o tempo em que seu processo admitiu preempção, mas ele fornece uma dica sobre o que criou a pressão de preempção contra seu processo.  
  
-   Avalie como o processo determina o número de threads adequado para execução durante essa fase de trabalho. Se o seu processo calcular diretamente o número de threads paralelos ativos, considere modificar esse algoritmo para representar melhor o número de núcleos lógicos disponíveis no sistema. Se você usar o Tempo de Execução de Simultaneidade, a biblioteca de paralelismo de tarefas ou PLINQ, essas bibliotecas realizam o trabalho de calcular o número de threads.  
  
## <a name="inefficient-io"></a>E/S ineficiente  
 ![E&#47;S ineficiente](../profiling/media/inefficient-io.png "Inefficient_IO")  
  
 O uso excessivo ou incorreto de E/S é uma causa comum de ineficiências em aplicativos. Considere a ilustração anterior. O Perfil da Linha de Tempo Visível mostra que 42 por cento do tempo de thread visível é consumido por E/S. A linha de tempo mostra grandes quantidades de E/S, que indica que o aplicativo analisado é frequentemente bloqueado por E/S. Para ver detalhes sobre os tipos de E/S e onde o seu programa está bloqueado, amplie as regiões problemáticas, examine o Perfil da Linha de Tempo Visível e, em seguida, clique em um bloco de E/S específico para ver as pilhas de chamadas atuais.  
  
## <a name="lock-convoys"></a>Comboios de bloqueio  
 ![Comboios de bloqueio](../profiling/media/lock-convoys.png "Lock_Convoys")  
  
 Comboios de bloqueio ocorrem quando o aplicativo adquire bloqueios em ordem de chegada e quando a taxa de chegada no bloqueio é maior que a taxa de aquisição. A combinação dessas duas condições faz com que as solicitações do bloqueio comecem a fazer backup. Uma maneira de combater esse problema é usar bloqueios “desleais” ou bloqueios que dão acesso ao primeiro thread para localizá-los em estados desbloqueados. A ilustração anterior mostra o comportamento desse comboio. Para resolver o problema, experimente reduzir a contenção dos objetos de sincronização e usar bloqueios desleais.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)



