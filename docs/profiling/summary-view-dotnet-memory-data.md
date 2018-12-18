---
title: Exibição Resumo – Dados da memória do .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Summary view
ms.assetid: 0cb317c3-0ae6-4531-aaa8-447576eec037
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 98b56eece1a51db94482a0a58d54ca877e47e0c1
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668118"
---
# <a name="summary-view---net-memory-data"></a>Exibição Resumo – dados de memória do .NET
A exibição Resumo exibe informações sobre as funções e os tipos do .NET que alocaram a maior quantidade de memória e os tipos que foram criados mais vezes em uma execução de criação de perfil. Para obter mais informações, incluindo uma descrição das listas de Links de Notificação e Relatório, confira [Exibição Resumo](../profiling/summary-view.md).  
  
## <a name="timeline-graph"></a>Gráfico de linha do tempo  
 O gráfico de linha do tempo na exibição Resumo mostra a utilização do processador (CPU) pelo aplicativo com perfil ao longo do tempo em que ocorreu a criação de perfil. É possível usar o gráfico de linha do tempo para filtrar a exibição para um intervalo de tempo selecionado. Para obter mais informações, confira [Como filtrar exibições de relatório por meio da Linha do Tempo de Resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md).  
  
## <a name="functions-allocating-most-memory"></a>Funções que Alocam Mais Memória  
 Lista as funções que alocaram o maior número de bytes de memória na execução de criação de perfil.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome da função.|  
|**% de bytes**|O percentual de todos os bytes alocados na execução de criação de perfil que foram alocados por essa função ou por uma função filho chamada por essa função.|  
  
## <a name="types-with-most-memory-allocated"></a>Tipos com mais memória alocada  
 Lista os tipos para os quais o maior número de bytes de memória foi alocado na execução de criação de perfil.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do tipo.|  
|**% de bytes**|O percentual de todos os bytes alocados na execução de criação de perfil que foram alocados para esse tipo.|  
  
## <a name="types-with-most-instances"></a>Tipos com mais instâncias  
 Lista os tipos que foram criados mais vezes durante a execução de criação de perfil. tinha  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do tipo.|  
|**% de instâncias**|O percentual do número total de objetos do .NET que foram criados na execução de criação de perfil que eram instâncias desse tipo.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Resumo – dados de amostragem](../profiling/summary-view-sampling-data.md)   
 [Exibição Resumo – dados de instrumentação](../profiling/summary-view-instrumentation-data.md)