---
title: Exibição de chamado-computador chamado – Dados de instrumentação da memória do .NET | Microsoft Docs
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
- Caller/Callee view
ms.assetid: da624c06-8741-4afb-aad1-f8c0002f3de2
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cf809747bff2146c6a45afd49768dbda69ae7d91
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782278"
---
# <a name="callercallee-view---net-memory-instrumentation-data"></a>Exibição Chamador/Receptor da Chamada – dados de instrumentação da memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modo de exibição de Chamador/Computador Chamado dos dados de criação de perfil de memória do .NET coletados usando o método de instrumentação exibe dados de alocação e de tempo para uma função selecionada e as funções pai e filho da função selecionada. A exibição de Chamador/Computador Chamado contém três grades.  
  
 A **Função atual** é exibida na grade do meio exibe informações de criação de perfil de memória sobre a função selecionada. Os valores incluem todas as chamadas amostradas para a função.  
  
 **Funções que chamaram a função atual** são exibidas na grade superior e mostram a quantidade do valor da função selecionada (atual) gerado por chamadas da função do chamador (pai).  
  
 **Funções que foram chamadas pela função atual** são exibidas na grade inferior e mostram dados de criação de perfil de memória para as funções do computador chamado (filho) da função selecionada quando a função filho foi chamada pela função atual.  
  
 Clique duas vezes em uma linha de função de chamador ou computador chamado para tornar essa linha a função atual.  
  
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
|**ID do Processo**|A ID de processo da execução de criação de perfil.|  
|**Nome do Processo**|O nome atribuído ao processo.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e suas funções filho causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
|**Tipo**|O contexto da função:<br /><br /> **0** – a função atual<br /><br /> **1** – uma função que chama a função atual<br /><br /> **2** – uma função que é chamada pela função atual<br /><br /> Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Nome da Função Raiz**|O nome da função atual. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
  
## <a name="net-memory-allocation-values"></a>Valores de Alocação de Memória do .NET  
  
|Column|Descrição|  
|------------|-----------------|  
|**Alocações Exclusivas**|–   Para a função atual, o número de objetos que foram criados quando a função estava executando código no corpo da função (isto é, quando a função estava na parte superior da pilha de chamadas). O número não inclui objetos que foram criados em funções que foram chamadas por essa função.<br />–   Para uma função do chamador, o número das alocações exclusivas da função atual que foram geradas por chamadas dessa função do chamador.<br />–   Para uma função do computador chamado, o número de objetos criados por instâncias dessa função que foram chamados pela função atual. Esse número não inclui os objetos alocados por funções criadas pela função do computador chamado.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos criados na execução de criação de perfil que eram alocações exclusivas dessa função.|  
|**Alocações Inclusivas**|–   Para a função atual, o número de objetos que foram alocados pela função na execução de criação de perfil. O número inclui objetos que foram criados nas funções do computador chamado chamadas pelas função.<br />–   Para uma função do chamador, o número das alocações inclusivas da função atual que foram geradas por chamadas dessa função do chamador.<br />–   Para uma função do computador chamado, o número de objetos alocados pelas instâncias dessa função que foram gerados por chamadas da função atual. O número inclui alocações feitas por funções que foram chamadas por essa função do computador chamado.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram criados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Bytes Exclusivos**|–   Para a função atual, o número de bytes de memória que foram alocados pela função na execução de criação de perfil. O número não inclui memória foi alocada em funções do computador chamado que foram chamadas pela função.<br />–   Para uma função do chamador, o número de bytes exclusivos da função atual que foram gerados por chamadas por essa função do chamador.<br />–   Para uma função do computador chamado, o número de bytes alocados pelas instâncias dessa função que foram gerados por chamadas da função atual. O número não inclui os bytes alocados por funções chamadas pela função do computador chamado.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações exclusivas dessa função.|  
|**Bytes Inclusivos**|–   Para a função atual, o número de bytes na memória que foram alocados pela função na execução de criação de perfil. O número inclui memória foi alocada em funções do computador chamado que foram chamadas pela função.<br />–   Para uma função do chamador, o número de bytes inclusivos das instâncias da função atual que foram gerados por chamadas dessa função do chamador.<br />–   Para uma função do computador chamado, o número de bytes alocados pelas instâncias dessa função que foram gerados por chamadas da função atual. O número inclui os bytes alocados por funções chamadas por essa função do computador chamado.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|–   Para a função atual, o tempo gasto na função. O valor inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />–   Para uma função do chamador, a quantidade de tempo inclusivo decorrido do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto nessa função que foi gerado por chamadas da função atual. O valor inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido dessa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo inclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo inclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo inclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo inclui o tempo em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas não inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|–   Para a função atual, o tempo gasto na execução do corpo da função. O valor exclui tempo gasto em funções filho, mas inclui chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.<br />–   Para uma função do chamador, a quantidade de tempo exclusivo decorrido do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto nessa função que foi gerado por chamadas da função atual. O valor exclui o tempo gasto em funções filho da função do computador chamado, mas inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total dessa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo exclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo exclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo exclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|–   Para a função atual, o tempo gasto na função e suas funções filho. O valor exclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />–   Para uma função do chamador, a quantidade de tempo inclusivo do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />–   Para uma função de computador chamado, o tempo gasto nessa função e suas funções filho que foi gerado por chamadas da função atual. O valor não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo inclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo inclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo inclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo gasto na função, excluindo o tempo gasto em funções filho. O tempo indicado também exclui o tempo gasto em chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|–   Para a função atual, o tempo gasto na execução do corpo da função. O valor não inclui o tempo gasto em funções filho nem inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.<br />–   Para uma função do chamador, a quantidade de tempo exclusivo do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto nessa função que foi gerado por chamadas da função atual. O valor não inclui o tempo gasto em funções filho da função do computador chamado, nem inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo exclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo exclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo exclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição Chamador/Receptor da Chamada – dados de amostragem da memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)   
 [Exibição de chamador/computador chamado – dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)   
 [Exibição de chamador/computador chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)



