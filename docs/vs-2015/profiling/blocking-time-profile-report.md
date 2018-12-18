---
title: Relatório de perfil de tempo de bloqueio | Microsoft Docs
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
- vs.cv.threads.report.blocking
helpviewer_keywords:
- Concurrency Visualizer, Blocking Time Profile Report
ms.assetid: 3bc45af0-3ba6-4fa3-a336-be8e9ae95107
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 31be25e5fb41f2e7a92ee2c19803d74c442fcad4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807017"
---
# <a name="blocking-time-profile-report"></a>Bloqueando relatório de perfil de tempo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os Relatórios de Perfil fornecem dados de tempo de bloqueio agregados para pilhas de chamadas específicas para cada categoria de bloqueio (por exemplo, "E/S" ou "Sincronização"). O relatório de Preempção lista os processos que admiram preempção do processo atual junto com o número de instâncias de preempção. Para criar o relatório do perfil de bloqueio, a ferramenta coleta chamadas à API de bloqueio e acumula-as em uma árvore de pilhas de chamadas. Dados mostrados nesses relatórios variam pelo intervalo de tempo atual, por threads ocultos e os dois filtros a seguir que podem ser aplicados:  
  
- Se Apenas Meu Código for selecionado, serão apresentados somente os registros de ativação com código do usuário, mais um nível abaixo do código de usuário.  
  
- Se o valor de redução de Ruído for definido, pilhas agrupadas com uma frequência menor que a especificada serão ignoradas.  
  
  Expanda qualquer entrada de árvore de chamada para localizar a linha de código na qual o tempo de bloqueio é gasto. Para localizar a linha de origem para uma entrada, escolha **Exibir Origem** no menu de atalho. Para localizar a linha de código que chamou esta, no menu de atalho, escolha **Exibir Sites de Chamada**. Se apenas um site de chamada estiver disponível, o comando será conectado à linha de código realçada para o site de chamada. Se houver vários sites de chamada, o comando abrirá uma caixa de diálogo na qual você pode selecionar uma entrada e, em seguida, escolher o botão **Ir para origem** para localizar o site de chamada realçado. Geralmente, é mais útil para exibir código-fonte para o site de chamada que tem mais instâncias, mais tempo ou ambos.  
  
## <a name="blocking-time-report-columns"></a>Colunas do relatório de tempo de bloqueio  
 A tabela a seguir mostra as colunas para cada relatório de tempo de bloqueio.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|Nome|O nome da função para cada nível da pilha de chamadas.|  
|Instâncias|O número de instâncias da chamada de bloqueio para o período de tempo visível.|  
|Tempo de bloqueio inclusivo|O tempo total de bloqueio gasto para todas as pilhas acumuladas para esse nível de árvore de pilha de chamadas. O número inclusivo é a soma do tempo de bloqueio exclusivo para essa função e o tempo de bloqueio exclusivo para todos os nós filho.|  
|Tempo de bloqueio exclusivo|O tempo total de bloqueio gasto durante o qual essa função é o nível mais baixo da pilha de chamadas. Uma entrada da pilha de chamadas exclusiva que tem um alto tempo de bloqueio exclusivo pode ser uma função de interesse.|  
|Categoria de API/espera|Mostrado somente para funções do nível mais baixo da pilha de chamadas. Quando a assinatura da chamada de bloqueio é reconhecida, o nome da API do bloqueio é fornecido. Se a assinatura não for reconhecida, as informações relatadas pelo kernel serão fornecidas.|  
|Detalhes|O nome totalmente qualificado da função. Isso inclui a contagem de linha, quando disponível.|  
  
### <a name="synchronization"></a>Sincronização  
 O relatório de sincronização mostra as chamadas responsáveis por segmentos que estão bloqueando na sincronização e os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de sincronização](../profiling/synchronization-time.md)  
  
### <a name="sleep"></a>Sleep  
 O relatório de Suspensão mostra as chamadas responsáveis pelo tempo de bloqueio atribuído ao tempo gasto em suspensão e os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de suspensão](../profiling/sleep-time.md).  
  
### <a name="io"></a>E/S  
 O relatório de E/S mostra as chamadas responsáveis por segmentos que estão bloqueando E/S e os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de E/S (Exibição Threads)](../profiling/i-o-time-threads-view.md).  
  
### <a name="memory-management"></a>Gerenciamento de memória  
 O relatório de Gerenciamento de Memória mostra as chamadas responsáveis por segmentos que estão bloqueando operações de gerenciamento na memória e os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de gerenciamento de memória](../profiling/memory-management-time.md).  
  
### <a name="preemption"></a>Preempção  
 O relatório de Preempção lista os processos que admiram preempção do processo atual junto com o número de instâncias.  Você pode expandir cada processo para exibir os threads específicos que substituíram threads no processo atual e exibir uma divisão de instâncias de preempção por thread. Esse relatório de bloqueio é menos acionável que outros porque preempção normalmente é imposta sobre seu processo pelo sistema operacional e não por um problema no seu código. Para obter mais informações, consulte [Tempo de preempção](../profiling/preemption-time.md).  
  
### <a name="ui-processing"></a>Processamento de interface do usuário  
 O relatório de Processamento de interface do usuário mostra as chamadas responsáveis por bloquear segmentos que estão bloqueando em blocos de processamento de interface do usuário e os tempos de bloqueio agregados de cada pilha de chamadas. Para obter mais informações, consulte [Tempo de processamento de interface do usuário](../profiling/ui-processing-time.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)



