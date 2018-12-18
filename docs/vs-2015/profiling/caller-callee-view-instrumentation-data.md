---
title: Exibição de chamador/computador chamado – Dados de instrumentação | Microsoft Docs
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
ms.assetid: 0908d354-aa5c-4518-8631-e25b8e7649e5
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2bbba1d9e169f82c7c43907bae87894de1dbcb9f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51775778"
---
# <a name="callercallee-view---instrumentation-data"></a>Exibição de chamador/computador chamado – dados de instrumentação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição de Chamador/Computador Chamado exibe informações de criação de perfil sobre uma função selecionada e suas funções pai e filho na árvore de chamadas. A exibição de Chamador/Computador Chamado contém três grades.  
  
 **Função atual** é exibida na grade intermediária e mostra informações de criação de perfil sobre a função selecionada. Os valores incluem todas as chamadas feitas à função.  
  
 **Funções que chamaram a função atual** é exibido na grade superior e mostra informações de criação de perfil sobre funções de chamador (pai) da função selecionada. Os valores indicam a quantidade do valor da função atual que foi gerado por chamadas dessa função do chamador.  
  
 **Funções que foram chamadas pela função atual** é exibido na grade inferior e mostra informações de criação de perfil sobre instâncias das funções de computador chamado (filho) da função selecionada. Os valores indicam apenas o tempo gasto na função filho quando ela foi chamada pela função atual.  
  
## <a name="general"></a>Geral  
 As colunas gerais identificam a função em uma linha de exibição.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome da Função**|O nome da função.|  
|**Endereço da Função**|O endereço da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Número de Chamadas**|O número total de chamadas feitas para essa função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função que foi causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e suas funções filho que foi causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
|**Tipo**|O contexto da função:<br /><br /> **0** – a função atual<br /><br /> **1** – uma função que chama a função atual<br /><br /> **2** – uma função que é chamada pela função atual<br /><br /> Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Nome da Função Raiz**|O nome da função atual. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções filho e o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|–   Para a função atual, o tempo gasto na função. O valor inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />–   Para uma função do chamador, a quantidade de tempo inclusivo decorrido do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto em instâncias dessa função que foram geradas por chamadas da função atual. O valor inclui o tempo gasto em funções filho do computador chamado em chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido dessa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo inclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo inclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo inclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas não inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|–   Para a função atual, o tempo gasto na execução direta da função. O valor inclui o tempo gasto em funções filho e em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />–   Para uma função do chamador, a quantidade de tempo exclusivo decorrido do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto em instâncias dessa função que foram geradas por chamadas da função atual. O valor exclui o tempo gasto em funções filho da função do computador chamado, mas inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo decorrido total dessa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo exclusivo decorrido médio de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo exclusivo decorrido máximo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo exclusivo decorrido mínimo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto, mas inclui o tempo gasto em funções filho.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|–   Para a função atual, o tempo gasto na função e suas funções filho. O valor exclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br />–   Para uma função do chamador, a quantidade de tempo inclusivo do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto em instâncias dessa função que foram geradas por chamadas da função atual. O valor inclui o tempo gasto em funções filho da função do computador chamado, mas não inclui o tempo gasto em chamadas ao sistema operacional, como operações de entrada/saída e mudança de contexto.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo inclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo inclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo inclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo gasto na função. Isso exclui o tempo gasto em funções filho e também exclui as chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|–   Para a função atual, o tempo gasto na execução direta da função. O valor não inclui o tempo gasto em funções filho nem inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.<br />–   Para uma função do chamador, a quantidade de tempo exclusivo do aplicativo da função atual que foi gerado por chamadas dessa função do chamador.<br />-   Para uma função de computador chamado, o tempo gasto em instâncias dessa função que foram geradas por chamadas da função atual. O valor não inclui o tempo gasto em funções filho da função do computador chamado, nem inclui chamadas ao sistema operacional, como mudanças de contexto e operações de entrada/saída.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo exclusivo decorrido total da execução da criação de perfil que foi gasto no tempo exclusivo do aplicativo total dessa função nesse contexto.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo exclusivo médio do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo exclusivo máximo do aplicativo de uma chamada para essa função nesse contexto.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo exclusivo mínimo do aplicativo de uma chamada para essa função nesse contexto.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição de chamador/computador chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)   
 [Exibição Chamador/Receptor da Chamada – dados de amostragem da memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)   
 [Exibição Chamador/Receptor da Chamada – dados de instrumentação da memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)



