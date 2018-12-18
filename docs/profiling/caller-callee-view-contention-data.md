---
title: Modo de Exibição de Chamador/Receptor - Dados de Contenção | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Caller/Callee view
ms.assetid: a18a1b1b-9b39-43c7-b1f3-708fd20376f6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f919bd6b3fdad1a9c7412960e14d8c9f4cf5af67
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34263144"
---
# <a name="callercallee-view----contention-data"></a>Exibição do Chamador/Receptor– dados de contenção
Modo de exibição do Chamador/Receptor exibe informações de contenção para uma função selecionada e suas funções pai e filho. A exibição de Chamador/Computador Chamado contém três grades.  
  
 A **função atual** é exibida na grade intermediária e mostra informações de contenção para a função selecionada. Os valores incluem todas os contenções de bloqueio para a função.  
  
 **Funções que chamaram a função atual** é exibido na grade superior e mostra as contribuições individuais das funções de chamador (pai) para os valores da função selecionada (atual).  
  
 As **funções que foram chamadas pela função atual** são exibidas na grade inferior e mostram informações de contenção para as funções do receptor (filho) da função selecionada quando a função filho foi chamada pela função atual.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tipo**|O contexto da função:<br /><br /> -   **0** – a função atual<br />-   **1** – uma função que chama a função atual<br />-   **2** – uma função que é chamada pela função atual<br /><br /> Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Tempo Bloqueado Exclusivo**|-Para a função atual, a hora em que essa função foi impedida de executar o código no corpo da função. Não inclui o tempo bloqueado nas funções chamadas pela função.<br />-Para uma função do chamador, a parte do tempo bloqueado exclusivo da função atual que ocorreram quando essa função de chamada de função atual.<br />-Para uma função do chamador, a hora em que essa função foi impedida de executar seu próprio código quando essa função foi chamada pela função atual. O tempo bloqueado em funções filho chamadas pela função receptor não está incluído.|  
|**% de Tempo Bloqueado Exclusivo**|A porcentagem de tempo bloqueado todos na criação de perfil que era tempo bloqueado exclusivo para esta função neste contexto.|  
|**Contenções Exclusivas**|-Para a função atual, o número de vezes que essa função foi impedida de executar o código no corpo da função. As contenções que ocorreram nas funções que foram chamadas pelas função não são incluídas nos valores exclusivos.<br />– Para uma função do chamador, o número de contenções exclusivas da função atual que ocorreram quando essa função chamou a função atual.<br />-Para uma função do chamador, o número de vezes que essa função foi impedida de executar o código no corpo da função quando essa função foi chamada pela função atual. As contenções que ocorreram em funções chamadas pela função de receptor não são incluídas.|  
|**% de Contenções Exclusivas**|A porcentagem de todas as contenções na criação de perfil que eram contenções exclusivas para esta função neste contexto.|  
|**Endereço da Função**|O endereço ou o token da função.|  
|**Nome da Função**|O nome totalmente qualificado da função.|  
|**Tempo Bloqueado Inclusivo**|-Para a função atual, a hora em que essa função ou uma das funções que foram chamadas por essa função foi impedida de executar. Inclui o tempo bloqueado nas funções que foram chamadas pela função atual.<br />-Para uma função do chamador, a parte do inclusivo bloqueadas tempo da função atual que ocorreram quando essa função de chamada de função atual.<br />-Para uma função do chamador, a hora em que essa função ou uma das funções que foi chamada pela função foi impedida de executar quando essa função foi chamada pelo atual funcionar. Inclui o tempo bloqueado nas funções que foram chamadas pela função do receptor.|  
|**% de Tempo Bloqueado Inclusivo**|O percentual de todo o tempo bloqueado na execução da criação de perfil que representou o tempo bloqueado inclusivo para esta função neste contexto.|  
|**Contenções Inclusivas**|-Para a função atual, o número de vezes que essa função ou uma das funções que foram chamadas pela função foi impedida de executar. As contenções que ocorreram nas funções que foram chamadas pelas função são incluídas nos valores exclusivos.<br />–   Para uma função do chamador, o número de contenções inclusivas da função atual que foram coletadas quando essa função chamou a função atual.<br />-Para uma função do chamador, o número de vezes que essa função ou uma das funções que foram chamadas pela função foi impedida de executar quando essa função foi chamada pela função atual. As contenções que ocorreram em funções chamadas pela função de receptor são incluídas.|  
|**% de Contenções Inclusivas**|A porcentagem de todas as contenções na criação de perfil que eram contenções exclusivas para esta função neste contexto.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A identificação do processo (PID) no qual as contenções ocorreram.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome da Função Raiz**|O nome da função atual. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de visualização de relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição do Chamador/Receptor](../profiling/caller-callee-view.md)   
 [Exibição do chamador/chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)   
 [Exibição do Chamador/Receptor – dados de instrumentação da memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)   
 [Exibição do Chamador/Receptor – dados de amostragem da memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)   
 [Exibição do Chamador/Receptor – dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)