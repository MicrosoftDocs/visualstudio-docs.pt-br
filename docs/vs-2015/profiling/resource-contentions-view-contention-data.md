---
title: Exibição de contenções de recurso – Dados de contenção | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.view.resourcecontention
helpviewer_keywords:
- Resource Contentions view
ms.assetid: 14a7f774-211f-4ef8-af05-94d1c8f65d2f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dddc9c85731137c6499e976b4b571396af297f7a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810345"
---
# <a name="resource-contentions-view---contention-data"></a>Exibição de contenções de recurso – Dados de contenção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição Contenção de Recursos lista os dados de contenção para os recursos que estavam na fonte de eventos de contenção. Um evento de contenção ocorre quando uma função em um thread é forçada a aguardar o acesso ao recurso porque uma função em outro thread obteve acesso exclusivo ao recurso. Cada recurso é o nó raiz de uma árvore de chamadas que exibe os caminhos de execução de função que resultaram em eventos de contenção.  
  
## <a name="data-values"></a>Valores de dados  
  
### <a name="resource-values"></a>Valores de Recurso  
 Os dados em uma linha de recurso exibem o tempo total pelo qual o acesso ao recurso ficou bloqueado nos dados de criação de perfil e o número total de eventos de contenção que ocorreu devido a conflito de acesso a esse recurso. Valores inclusivos e exclusivos para um recurso são sempre os mesmos.  
  
### <a name="function-values"></a>Valores de Função  
 Valores de função são baseados nas instâncias da função que ocorreram no caminho de execução representado na árvore de chamadas.  
  
-   Valores exclusivos baseiam-se nos eventos que ocorreram quando a função estava executando instruções no corpo da função. Eventos que ocorreram nas funções que foram chamadas pelas função não são incluídos nos valores exclusivos.  
  
-   Valores inclusivos baseiam-se nos eventos que ocorreram quando a função ou uma função chamada por ela, estava em execução.  
  
### <a name="percentage-values"></a>Valores de percentual  
 Valores de percentual baseiam-se em eventos de tempo ou de contenção total nos dados de criação de perfil. Se o relatório ou a exibição da execução de criação de perfil for filtrado, somente o tempo bloqueado e as contenções nos dados filtrados serão usadas como o valor total.  
  
## <a name="navigating-the-resource-allocation-view"></a>Navegando pela Exibição de alocação de recurso  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do recurso ou da função.|  
|**Tempo Bloqueado Exclusivo**|-   Para um recurso, o tempo total que o acesso ao recurso foi bloqueado e fez o thread aguardar.<br />-   Para uma função, o tempo pelo qual essas instâncias da função foram impedidas de acessar o recurso pai quando a função estava executando código no corpo da função. Não inclui o tempo bloqueado nas funções que foram chamadas pela função.|  
|**% de Tempo Bloqueado Exclusivo**|-  Para um recurso, o percentual de todo o tempo bloqueado nos dados de criação de perfil que representou tempo bloqueado deste recurso<br />-   Para uma função, o percentual de todo o tempo bloqueado nos dados de criação de perfil que representou tempo bloqueado exclusivo dessas instâncias de função.|  
|**Contenções Exclusivas**|-   Para um recurso, o número total de vezes que o acesso ao recurso foi bloqueado e fez um thread aguardar.<br />-   Para uma função, o número de vezes que essas instâncias da função foram impedidas de acessar o recurso pai quando a função estava executando código no corpo da função. Não inclui o bloqueio de eventos em funções que foram chamadas pela função.|  
|**% de Contenções Exclusivas**|-   Para um recurso, o percentual de todos os eventos de contenção nos dados de criação de perfil que eram de contenção para acessar esse recurso.<br />-   Para uma função, o percentual de todos os eventos de contenção nos dados de criação de perfil que eram eventos de contenção exclusivos dessas instâncias de função para o recurso pai.|  
|**Tempo Bloqueado Inclusivo**|-   Para um recurso, o tempo total que o acesso ao recurso foi bloqueado e fez o thread aguardar.<br />-   Para uma função, o tempo pelo qual essas instâncias da função ou quaisquer funções chamadas pelas instâncias, foram impedidas de acessar o recurso pai quando a função estava executando código no corpo da função.|  
|**% de Tempo Bloqueado Inclusivo**|-  Para um recurso, o percentual de todo o tempo bloqueado nos dados de criação de perfil que representou tempo bloqueado deste recurso<br />-   Para uma função, o percentual de todo o tempo bloqueado na execução da criação de perfil que representou o tempo bloqueado inclusivo dessas instâncias de função.|  
|**Contenções Inclusivas**|-   Para um recurso, o número total de vezes que o acesso ao recurso foi bloqueado e fez um thread aguardar.<br />-   Para uma função, o percentual de todos os eventos de contenção na execução da criação de perfil que eram eventos de contenção inclusivos dessas instâncias de função para o recurso pai.|  
|**% de Contenções Inclusivas**|-   Para um recurso, o percentual de todos os eventos de contenção na execução da criação de perfil que eram de contenção para acessar esse recurso.<br />-   Para uma função, o número de vezes que essas instâncias da função foram impedidas de acessar o recurso pai quando a função estava executando código no corpo da função. Não inclui o bloqueio de eventos em funções que foram chamadas pela função.|  
|**Nível**|A profundidade dessa função na árvore de chamadas. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A PID (ID do processo) do processo no qual a função estava sendo executada.|  
|**Nome do Processo**|O nome do processo.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|



