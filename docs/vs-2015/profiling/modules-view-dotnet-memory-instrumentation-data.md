---
title: Exibição Módulos – Dados de instrumentação da memória do .NET | Microsoft Docs
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
- Modules view
ms.assetid: 26516139-0981-41de-917d-ad5769391b8d
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 85024296eff4fb4d26b3a588217a1e6fe5221d3e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755400"
---
# <a name="modules-view---net-memory-instrumentation-data"></a>Exibição Módulos – Dados de instrumentação da memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição Módulos de dados de alocação de memória do .NET coletados usando o método de instrumentação agrupa os dados de tempo e memória pelos módulos que foram executados na execução de criação de perfil. Os dados de criação de perfil das funções do módulo são listados abaixo do nó do módulo.  
  
## <a name="general"></a>Geral  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome da função ou módulo.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Número de Chamadas**|O número total de chamadas que foram feitas para essa função ou módulo.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo em que o módulo ou função estava sendo executada.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função ou módulo devido à instrumentação.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função ou módulo e suas funções filho devido à instrumentação.|  
  
## <a name="net-memory-values"></a>Valores de memória do .NET  
 Os valores de memória do .NET inclusivos de uma função indicam o número (alocações) e o tamanho (bytes) de objetos que foram criados pela função e suas funções filho.  
  
 Os valores de memória exclusivos indicam o número e tamanho dos objetos que foram criados pela função e não por suas funções filho.  
  
 Os valores de memória inclusivos e exclusivos de um módulo são a soma dos valores de memória inclusivos e exclusivos das funções no módulo.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Alocações Inclusivas**|– Para uma função, o número total de objetos que foram criados pela função. Esse número inclui objetos que foram criados por funções que foram chamadas pela função.<br />– Para um módulo, o número de objetos em uma execução de criação de perfil que foram alocados quando pelo menos uma função do módulo estava em execução. Esse número inclui objetos que foram alocados em funções que foram geradas por chamadas de funções do módulo.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram alocados na execução de criação de perfil que eram alocações inclusivas do módulo ou função.|  
|**Alocações Exclusivas**|– Para uma função, o número de objetos que foram criados quando a função estava executando código no corpo da função (isto é, quando a função estava na parte superior da pilha de chamadas). Esse número não inclui objetos que foram criados em funções que foram chamadas pela função.<br />– Para um módulo, a soma das alocações exclusivas das funções no módulo.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos que foram alocados na execução de criação de perfil que eram alocações exclusivas do módulo ou função.|  
|**Bytes Exclusivos**|– Para uma função, o número total de bytes de memória que foram alocados quando a função estava executando o código no corpo da função (isto é, quando a função estava na parte superior da pilha de chamadas). Esse número não inclui bytes que foram alocados em funções que foram chamadas pela função.<br />– Para um módulo, a soma dos bytes exclusivos que foram alocados pelas funções no módulo.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes que foram alocados na execução de criação de perfil que eram bytes exclusivos do módulo, função, linha ou instrução.|  
|**Bytes Inclusivos**|– Para uma função, o número de bytes que foram alocados pela função. Esse número inclui bytes que foram alocados em funções que foram chamadas pela função.<br />– Para um módulo, o número de bytes que foram alocados em uma execução de criação de perfil que foram alocados quando pelo menos uma função do módulo estava em execução. Esse número inclui objetos que foram criados em todas as funções que foram chamadas pelas funções do módulo.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes que foram alocados na execução de criação de perfil que eram bytes inclusivos do módulo ou função.|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|– Para uma função, o tempo gasto na função. Isso inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />– Para um módulo, o período em que pelo menos uma função no módulo estava na pilha de chamadas.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido total desse módulo ou função.|  
|**Tempo Inclusivo Decorrido Médio**|– Para uma função, o tempo inclusivo decorrido médio de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo decorrido médio de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Decorrido Máximo**|– Para uma função, o tempo inclusivo decorrido máximo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo decorrido máximo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Decorrido Mínimo**|– Para uma função, o tempo inclusivo decorrido mínimo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo inclusivo decorrido mínimo de todas as chamadas para funções no módulo.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O valor não inclui o tempo gasto em funções filho, mas inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|– Para uma função, o tempo gasto no módulo ou função. Isso inclui chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída, mas exclui o tempo que foi gasto em funções filho.<br />– Para um módulo, a soma dos tempos exclusivos decorridos das funções no módulo.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total desse módulo ou função.|  
|**Tempo Exclusivo Decorrido Médio**|– Para uma função, o tempo exclusivo decorrido médio de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo decorrido médio de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Decorrido Máximo**|– Para uma função, o tempo exclusivo decorrido máximo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo decorrido máximo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Decorrido Mínimo**|– Para uma função, o tempo exclusivo decorrido mínimo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo exclusivo decorrido mínimo de todas as chamadas para funções no módulo.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|– Para uma função, o tempo gasto em chamadas para a função. Isso inclui o tempo gasto em funções filho, mas exclui as chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.<br />– Para um módulo, o período em que pelo menos uma função no módulo estava na pilha de chamadas, exceto o tempo gasto em chamadas para o sistema operacional.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo desse módulo ou função.|  
|**Tempo Inclusivo Médio do Aplicativo**|– Para uma função, o tempo inclusivo médio do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo médio do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Máximo do Aplicativo**|– Para uma função, o tempo inclusivo máximo do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo máximo do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|– Para uma função, o tempo inclusivo mínimo do aplicativo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo inclusivo mínimo do aplicativo de todas as chamadas para funções no módulo.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo gasto no módulo ou função, excluindo o tempo gasto em funções filho. O tempo indicado também exclui as chamadas para o sistema operacional, como alterações de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|– Para uma função, o tempo exclusivo do aplicativo total de chamadas para essa função.<br />– Para um módulo, o tempo exclusivo do aplicativo total de todas as chamadas para funções no módulo.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo desse módulo ou função.|  
|**Tempo Exclusivo Médio do Aplicativo**|– Para uma função, o tempo exclusivo médio do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo médio do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Máximo do Aplicativo**|– Para uma função, o tempo exclusivo máximo do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo máximo do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|– Para uma função, o tempo exclusivo mínimo do aplicativo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo exclusivo mínimo do aplicativo de todas as chamadas para funções no módulo.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Módulos – amostragem](../profiling/modules-view-dotnet-memory-sampling-data.md)   
 [Exibição Módulos](../profiling/modules-view-instrumentation-data.md)   
 [Exibição Módulos](../profiling/modules-view-sampling-data.md)



