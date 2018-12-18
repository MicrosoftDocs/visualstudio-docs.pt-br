---
title: Exibição de alocações da memória do .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.allocation
helpviewer_keywords:
- performance reports, allocation view
- Allocations view
- profiling tools, Allocation view
- profiling tools reports, Allocation view
ms.assetid: 01eb876e-c413-4516-977b-4f896929e8a6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b7a473a7c6758fe58c82f8894822d3a250165a43
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933671"
---
# <a name="net-memory-allocations-view"></a>Exibição de alocações da memória do .NET
A exibição de Alocações lista os tipos criados durante a execução de criação de perfil. Cada tipo é o nó raiz de uma árvore de chamadas que exibe os caminhos de execução de função que resultaram em alocações do tipo.  
  
 Os dados em uma linha de tipo exibem o número total de objetos do tipo criados na execução de criação de perfil e o número total de bytes alocados para os objetos desse tipo. Os valores inclusivos e exclusivos para um tipo são sempre os mesmos.  
  
- Os valores inclusivos são para objetos criados nas instâncias da função e suas funções filho chamadas pela função pai na árvore de chamadas.  
  
- Os valores exclusivos são para objetos criados diretamente pela função quando foram chamados pela função pai. Objetos criados nas funções filho não são incluídos.  
  
  Os dados de uma função exibem o número de objetos criados e o número de bytes alocados para objetos do tipo pai.  
  
## <a name="highlight-the-execution-hot-path"></a>Realçar o afunilamento de execução  
 É possível encontrar o caminho de execução da árvore de chamadas que criou a maioria dos objetos do tipo pai.  
  
-   Para exibir o caminho mais ativo, clique com o botão direito do mouse no tipo ou na função e, em seguida, clique em **Expandir Afunilamento**.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do tipo alocado ou da função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém o tipo ou a função.|  
|**Caminho do Módulo**|O caminho do módulo que contém o tipo ou a função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição do tipo ou função.|  
|**Número de linha da função**|O número de linha do início dessa definição de tipo ou função no arquivo de origem.|  
|**Nível**|Indica se os dados são de um tipo ou uma função.|  
|**Alocações Inclusivas**|– Para uma função, o número total de objetos do tipo pai criados pela função. Esse número inclui objetos criados em funções filho.<br />– Para um tipo, o número total de instâncias desse tipo que foram criadas.|  
|**% de Alocações Inclusivas**|– Para uma função, o percentual de todos os objetos criados na execução de criação de perfil que eram alocações inclusivas do tipo pai pela função.<br />– Para um tipo, o percentual do número total de objetos do criados na execução de criação de perfil que eram instâncias do tipo.|  
|**Alocações Exclusivas**|– Para uma função, o número de objetos criados quando a função estava executando diretamente na parte superior da pilha de chamadas. Esse número não inclui objetos criados em funções filho.<br />– Para um tipo, o número total de instâncias desse tipo que foram criadas.|  
|**% de Alocações Exclusivas**|– Para uma função, o percentual de todos os objetos criados na execução de criação de perfil que eram alocações exclusivas do tipo pai pela função.<br />– Para um tipo, o percentual do número total de objetos do criados na execução de criação de perfil que eram instâncias do tipo.|  
|**Bytes Inclusivos**|– Para uma função, o número de bytes de memória alocados pela função para objetos do tipo pai. Esse número inclui a memória alocada por suas funções filho.<br />– Para um tipo, o número total de bytes alocados na execução de criação de perfil para as instâncias do tipo.|  
|**% de Bytes Inclusivos**|– Para uma função, o percentual de toda a memória alocada na execução de criação de perfil que eram alocações inclusivas do tipo pai pela função.<br />– Para um tipo, o percentual de toda a memória alocada na execução de criação de perfil que foi alocado em instâncias do tipo.|  
|**Bytes Exclusivos**|– Para uma função, o número de bytes de memória alocados pela função para objetos do tipo pai. Esse número não inclui a memória alocada por suas funções filho.<br />– Para um tipo, o número total de bytes alocados na execução de criação de perfil para as instâncias do tipo.|  
|**% de Bytes Exclusivos**|– Para uma função, o percentual de toda a memória alocada na execução de criação de perfil que eram alocações exclusivas do tipo pai pela função.<br />– Para um tipo, o percentual de toda a memória alocada na execução de criação de perfil que foi alocado em instâncias do tipo.|