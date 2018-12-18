---
title: Exibição Módulos – Dados de amostragem de memória do .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Modules view
ms.assetid: 9c05b51a-8382-44cf-a8f7-3fabdd2e8f1b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: c5cbae58aeaa1164aab6c254f62e0959da02d31c
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257667"
---
# <a name="modules-view---net-memory-sampling-data"></a>Exibição Módulos – dados de amostragem de memória do .NET
A exibição Módulos de dados de alocação de memória do .NET coletados usando o método de amostragem agrupa os dados de memória pelos módulos que foram executados na execução de criação de perfil. Cada módulo é a raiz de uma árvore hierárquica. As funções do módulo são listadas abaixo do nó do módulo.  
  
 Os números de linha de arquivo de origem de instruções que alocam memória são listados sob o nó de função e os endereços das instruções que fazem a alocação são listados sob o nó de linha. Os valores exclusivos e inclusivos são sempre os mesmos para dados de linha e dados de instrução.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do módulo, função, número de linha ou endereço de instrução.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O caminho do módulo.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Alocações Inclusivas**|– Para uma função, o número total de objetos que foram criados pela função. O número inclui objetos que foram criados em funções que foram chamadas por essa função.<br />– Para um módulo, o número de objetos em uma execução de criação de perfil que foram alocados enquanto pelo menos uma função do módulo estava em execução. O número inclui objetos que foram criados nas funções que foram chamadas pelas funções do módulo.<br />– Para uma linha ou instrução, o número total de objetos que foram alocados pela linha ou instrução.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram alocados na execução de criação de perfil que eram alocações inclusivas do módulo, função, linha ou instrução.|  
|**Alocações Exclusivas**|– Para a função atual, o número de objetos que foram criados quando a função estava executando código do corpo da função (isto é, quando a função estava na parte superior da pilha de chamadas). O número não inclui objetos que foram criados em funções que foram chamadas por essa função.<br />– Para um módulo, a soma das alocações exclusivas das funções no módulo.<br />– Para uma linha ou instrução, o número total de objetos que foram criados por essa linha ou instrução.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos que foram alocados na execução de criação de perfil que eram alocações exclusivas do módulo, função, linha ou instrução.|  
|**Bytes Inclusivos**|– Para uma função, o número de bytes que foram alocados pela função. O número inclui bytes que foram alocados em funções que foram chamadas por essa função.<br />– Para um módulo, o número de bytes que foram alocados em uma execução de criação de perfil que foram alocados enquanto pelo menos uma função do módulo estava em execução. O número inclui objetos que foram criados em todas as funções que foram chamadas pelas funções do módulo.<br />– Para uma linha ou instrução, o número total de objetos que foram criados pela linha ou instrução.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes que foram alocados na execução de criação de perfil que eram bytes inclusivos do módulo, função, linha ou instrução.|  
|**Bytes Exclusivos**|– Para uma função, o número total de bytes que foram alocados pela função. O número não inclui bytes que foram alocados em funções que foram chamadas por essa função.<br />– Para um módulo, a soma dos bytes exclusivos que foram alocados pelas funções no módulo.<br />– Para uma linha ou instrução, o número total de objetos que foram alocados por essa linha ou instrução.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes que foram alocados na execução de criação de perfil que eram bytes exclusivos do módulo, função, linha ou instrução.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição Módulos – instrumentação](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [Exibição Módulos](../profiling/modules-view-sampling-data.md)   
 [Exibição Módulos](../profiling/modules-view-instrumentation-data.md)