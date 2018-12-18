---
title: Exibição Módulos – Dados de amostragem de memória do .NET | Microsoft Docs
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
ms.assetid: 9c05b51a-8382-44cf-a8f7-3fabdd2e8f1b
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0b9a02e5579eb5dc82f2e1f21a10444c329a317f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51765533"
---
# <a name="modules-view---net-memory-sampling-data"></a>Exibição Módulos – Dados de amostragem de memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição Módulos – Instrumentação](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [Exibição Módulos](../profiling/modules-view-sampling-data.md)   
 [Exibição Módulos](../profiling/modules-view-instrumentation-data.md)



