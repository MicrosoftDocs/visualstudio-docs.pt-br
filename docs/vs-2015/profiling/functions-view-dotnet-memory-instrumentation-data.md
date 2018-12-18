---
title: Exibição Funções – Dados de instrumentação da memória do .NET | Microsoft Docs
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
- Functions view
ms.assetid: cd45b379-394b-4b71-828c-92cd89e46ae0
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8bacc61ec9c254ce662854a08fe6a508977a72e2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730181"
---
# <a name="functions-view---net-memory-instrumentation-data"></a>Exibição Funções – Dados de instrumentação de memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição Funções dos dados de criação de perfil de alocação de memória do .NET que foram coletados usando o método de instrumentação lista as funções que alocaram memória durante a execução da criação de perfil. Uma linha de função informa o tamanho e o número de alocações e dados de temporização para a função.  
  
## <a name="general"></a>Geral  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome da Função**|O nome da função.|  
|**Endereço da Função**|O endereço da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Número de Chamadas**|O número total de chamadas que são feitas à função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e suas funções filho causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
  
## <a name="net-memory-values"></a>Valores de memória do .NET  
 Os valores de memória do .NET inclusivos de uma função indicam o número (alocações) e o tamanho (bytes) de objetos que foram criados pela função e suas funções filho.  
  
 Os valores de memória exclusivos indicam o número e tamanho dos objetos que foram criados pela função e não por suas funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Alocações Inclusivas**|O número total de objetos que foram criados nesta função e em funções que foram chamadas por essa função.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram alocados na execução da criação de perfil que eram alocações inclusivas dessa função.|  
|**Alocações Exclusivas**|O número total de objetos que foram criados quando a função executou código no corpo da função. Esse número não inclui objetos que foram criados em funções que foram chamadas por essa função.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos criados na execução de criação de perfil que eram alocações exclusivas dessa função.|  
|**Bytes Inclusivos**|O número de bytes da memória que foram alocados nesta função e em funções que foram chamadas por essa função.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram bytes inclusivos dessa função.|  
|**Bytes Exclusivos**|O número de bytes da memória que foram alocados nesta função, mas não em funções que foram chamadas por essa função.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram bytes exclusivos dessa função.|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|O tempo inclusivo decorrido total de todas as chamadas feitas a essa função.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido dessa função.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo inclusivo decorrido médio de uma chamada feita para essa função.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo inclusivo decorrido máximo de uma chamada feita a essa função.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo inclusivo decorrido mínimo de uma chamada feita a essa função.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo inclui o tempo em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas não inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|O tempo exclusivo decorrido total de todas as chamadas feitas a essa função.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total dessa função.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo exclusivo decorrido médio de uma chamada feita para essa função.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo exclusivo decorrido máximo de uma chamada feita a essa função.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo exclusivo decorrido mínimo de uma chamada feita a essa função.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|O tempo inclusivo do aplicativo total de todas as chamadas para essa função.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo total dessa função.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo inclusivo médio do aplicativo de uma chamada para essa função.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo inclusivo máximo do aplicativo de uma chamada para essa função.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo inclusivo mínimo do aplicativo de uma chamada para essa função.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, nem o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|O tempo exclusivo do aplicativo total de todas as chamadas para essa função.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo total dessa função.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo exclusivo médio do aplicativo de uma chamada para essa função.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo exclusivo máximo do aplicativo de uma chamada para essa função.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo exclusivo mínimo do aplicativo de uma chamada para essa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição de Funções – Amostragem](../profiling/functions-view-dotnet-memory-sampling-data.md)   
 [Exibição de Funções](../profiling/functions-view-instrumentation-data.md)   
 [Exibição Funções](../profiling/functions-view-sampling-data.md)



