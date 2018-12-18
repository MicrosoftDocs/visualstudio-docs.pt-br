---
title: Exibição Módulos – dados de instrumentação | Microsoft Docs
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
ms.assetid: 895b9589-1987-4160-916f-53b898a69cf0
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 55a01dab80d15bcd7356bc059db2be6d10f504a7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51808506"
---
# <a name="modules-view---instrumentation-data"></a>Exibição Módulos – dados de instrumentação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição Módulos mostra dados de desempenho agrupados pelos módulos que estavam nos dados de criação de perfil. As funções do módulo são listadas abaixo do nó do módulo.  
  
## <a name="general"></a>Geral  
 As colunas gerais identificam a função em uma linha de exibição.  
  
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
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|– Para uma função, o tempo gasto na função. Isso inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />– Para um módulo, o tempo em que pelo menos uma função no módulo estava na pilha de chamadas.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido total desse módulo ou função.|  
|**Tempo Inclusivo Decorrido Médio**|– Para uma função, o tempo inclusivo decorrido médio de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo decorrido médio de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Decorrido Máximo**|– Para uma função, o tempo inclusivo decorrido máximo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo decorrido máximo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Decorrido Mínimo**|– Para uma função, o tempo inclusivo decorrido mínimo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo inclusivo decorrido mínimo de todas as chamadas para funções no módulo.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas não inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|– Para uma função, o tempo gasto no módulo ou função. Isso inclui chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída, mas exclui o tempo que foi gasto em funções filho.<br />– Para um módulo, a soma dos tempos exclusivos decorridos das funções no módulo.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total desse módulo ou função.|  
|**Tempo Exclusivo Decorrido Médio**|– Para uma função, o tempo exclusivo decorrido médio de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo decorrido médio de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Decorrido Máximo**|– Para uma função, o tempo exclusivo decorrido máximo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo decorrido máximo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Decorrido Mínimo**|– Para uma função, o tempo exclusivo decorrido mínimo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo exclusivo decorrido mínimo de todas as chamadas para funções no módulo.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. No entanto, o tempo inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|– Para uma função, o tempo gasto em chamadas para a função. Isso inclui o tempo gasto em funções filho, mas exclui as chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.<br />– Para um módulo, o tempo em que pelo menos uma função no módulo estava na pilha de chamadas. Isso exclui o tempo gasto em chamadas para o sistema operacional.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo desse módulo ou função.|  
|**Tempo Inclusivo Médio do Aplicativo**|– Para uma função, o tempo inclusivo médio do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo médio do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Máximo do Aplicativo**|– Para uma função, o tempo inclusivo máximo do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo inclusivo máximo do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|– Para uma função, o tempo inclusivo mínimo do aplicativo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo inclusivo mínimo do aplicativo de todas as chamadas para funções no módulo.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo gasto no módulo ou função. Isso exclui o tempo gasto em funções filho e também exclui as chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|O tempo exclusivo do aplicativo total de todas as chamadas para esse módulo ou função.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo desse módulo ou função.|  
|**Tempo Exclusivo Médio do Aplicativo**|– Para uma função, o tempo exclusivo médio do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo médio do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Máximo do Aplicativo**|– Para uma função, o tempo exclusivo máximo do aplicativo de uma chamada para essa função.<br />– Para um módulo, o tempo exclusivo máximo do aplicativo de todas as chamadas para funções no módulo.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|– Para uma função, o tempo exclusivo mínimo do aplicativo de uma chamada para esse módulo ou função.<br />– Para um módulo, o tempo exclusivo mínimo do aplicativo de todas as chamadas para funções no módulo.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Módulos](../profiling/modules-view-sampling-data.md)   
 [Exibição Módulos – Instrumentação](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [Exibição Módulos – amostragem](../profiling/modules-view-dotnet-memory-sampling-data.md)



