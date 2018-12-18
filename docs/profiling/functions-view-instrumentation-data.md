---
title: Exibição de Funções – Dados de Instrumentação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Function view
ms.assetid: 595d91c8-a42b-4644-85b8-39e8140a5dfe
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7787e974b093156b27b2ace4353e94db05063d7d
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35238219"
---
# <a name="functions-view---instrumentation-data"></a>Exibição funções – dados de instrumentação
A exibição de relatório de Funções lista dados de criação perfil segundo o nome da função.  
  
## <a name="general"></a>Geral  
 As colunas gerais identificam a função em uma linha de exibição.  
  
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
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função que é causada pela instrumentação. Não inclui a sobrecarga nas funções que foram chamadas pela função. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e as respectivas funções filho que é causada pela instrumentação. Inclui a sobrecarga nas funções que foram chamadas pela função. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
  
## <a name="elapsed-inclusive-values"></a>Valores inclusivos decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. Inclui o tempo que foi gasto em funções que foram chamadas pela função e o tempo foi gasto em chamadas para o sistema operacional, como operações de entrada/saída e de alternância de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|O tempo inclusivo decorrido total de todas as chamadas feitas a essa função.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido dessa função.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo inclusivo decorrido médio de uma chamada feita para essa função.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo inclusivo decorrido máximo de uma chamada feita a essa função.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo inclusivo decorrido mínimo de uma chamada feita a essa função.|  
  
## <a name="elapsed-exclusive-values"></a>Valores exclusivos decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava executando código no corpo da função, ou seja, quando a função estava no topo da pilha de chamadas. Inclui o tempo que foi gasto em chamadas para o sistema operacional, como operações de entrada/saída e de alternância de contexto, mas não inclui o tempo gasto em funções que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|O tempo exclusivo decorrido total de todas as chamadas feitas a essa função.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total dessa função.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo exclusivo decorrido médio de uma chamada feita para essa função.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo exclusivo decorrido máximo de uma chamada feita a essa função.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo exclusivo decorrido mínimo de uma chamada feita a essa função.|  
  
## <a name="application-inclusive-values"></a>Valores inclusivos do aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. Não inclui o tempo que foi gasto em chamadas para o sistema operacional, como operações de entrada/saída e de alternância de contexto, mas inclui o tempo gasto em funções que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|O tempo inclusivo do aplicativo total de todas as chamadas para essa função.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo total dessa função.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo inclusivo médio do aplicativo de uma chamada para essa função.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo inclusivo máximo do aplicativo de uma chamada para essa função.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo inclusivo mínimo do aplicativo de uma chamada para essa função.|  
  
## <a name="application-exclusive-values"></a>Valores exclusivos do aplicativo  
 Valores exclusivos do aplicativo indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. Não inclui o tempo que foi gasto em chamadas para o sistema operacional, como operações de entrada/saída e de alternância de contexto e não inclui o tempo gasto em funções que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|O tempo exclusivo do aplicativo total de todas as chamadas para essa função.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo total dessa função.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo exclusivo médio do aplicativo de uma chamada para essa função.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo exclusivo máximo do aplicativo de uma chamada para essa função.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo exclusivo mínimo do aplicativo de uma chamada para essa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição de Funções](../profiling/functions-view-sampling-data.md)   
 [Exibição Funções – amostragem](../profiling/functions-view-dotnet-memory-sampling-data.md)   
 [Exibição Funções – instrumentação](../profiling/functions-view-dotnet-memory-instrumentation-data.md)