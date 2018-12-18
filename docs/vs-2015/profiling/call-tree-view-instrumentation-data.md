---
title: Modo de exibição de árvore de chamadas – Dados de instrumentação | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Call Tree view
ms.assetid: 306bd176-0ce9-4a10-89ca-20b043d37d4e
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 630f75468adf5995eb887ac5f73d82462bfe32a4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786232"
---
# <a name="call-tree-view---instrumentation-data"></a>Modo de exibição de árvore de chamadas – Dados de instrumentação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os valores para uma função na árvore de chamadas indicam a hora para as instâncias de função chamadas pela função pai na árvore de chamadas. Valores de percentual são calculados comparando o valor das instâncias de função com o tempo inclusivo decorrido total de todas as funções na execução de criação de perfil.  
  
## <a name="general"></a>Geral  
 As colunas gerais identificam a função em uma linha de exibição.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome da Função**|O nome da função.|  
|**Endereço da Função**|O endereço da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Número de Chamadas**|O número total de chamadas feitas a essa função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome atribuído ao processo.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função que foi causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e suas funções filho que foi causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
|**Nível**|A profundidade da função na árvore de chamadas. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Valores inclusivos decorridos indicam o tempo na pilha de chamadas dessas instâncias da função que foram chamadas pela função pai na árvore de chamadas. O tempo inclui o tempo gasto em funções filho chamadas pela função e em chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|O tempo inclusivo decorrido total de todas as chamadas feitas a essa função nesse contexto.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido total dessa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo inclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo inclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo inclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo que as instâncias de uma função chamadas pela função pai na árvore de chamadas estavam executando código no corpo da função; ou seja, quando a função estava na parte superior da pilha de chamadas. O tempo inclui o tempo em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. No entanto, o tempo não inclui o tempo gasto em funções filho que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|O tempo exclusivo decorrido total de todas as chamadas para essa função nesse contexto.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total dessa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo exclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo exclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo exclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Valores inclusivos do aplicativo indicam o horário em que instâncias de uma função chamadas pela função pai na árvore de chamadas estavam na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. Porém, inclui o tempo gasto em funções filho chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|O tempo inclusivo do aplicativo total de todas as chamadas para essa função nesse contexto.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo inclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo inclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo inclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o horário em que as instâncias de uma função chamadas pela função pai na árvore de chamadas estavam diretamente executando código no corpo da função; ou seja, quando a função estava na parte superior da pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. Também não inclui o tempo gasto em funções filho que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|O tempo exclusivo do aplicativo total de todas as chamadas para essa função nesse contexto.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo exclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo exclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo exclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Modo de exibição de árvore de chamadas](../profiling/call-tree-view-sampling-data.md)   
 [Modo de exibição de árvore de chamadas – instrumentação](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)   
 [Modo de exibição de árvore de chamadas – amostragem](../profiling/call-tree-view-dotnet-memory-sampling-data.md)



