---
title: Regras de Desempenho do Monitoramento de Recurso | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 433a89ae2a7cf8c9e20ec3711dcebe1514ae021b
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31584575"
---
# <a name="resource-monitoring-performance-rules"></a>Regras de desempenho do monitoramento de recurso
As mensagens de desempenho da categoria Monitoramento de Recurso fornecem dados adicionais sobre o desempenho do aplicativo. É possível utilizar esses dados para analisar problemas de desempenho. Essas regras são informativas e relatadas para todas as execuções de criação de perfil.  
  
|||  
|-|-|  
|[DA0501: consumo de CPU médio pelo processo com perfil sendo criado.](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|  
|[DA0502: consumo de CPU máximo pelo processo com perfil sendo criado](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual máximo de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é o valor máximo relatado entre todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|  
|[DA0503: conjunto de trabalho médio em bytes para o processo cujo perfil está sendo criado](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória física em bytes que o processo usou enquanto a criação de perfil estava ativa. Essa medida de memória física é conhecida como conjunto de trabalho.|  
|[DA0504: conjunto de trabalho máximo em bytes para o processo cujo perfil está sendo criado](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória física em bytes que o processo estava usando durante a criação de perfil.|  
|[DA0505: média de bytes particulares alocados para o processo cujo perfil está sendo criado](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória virtual que o processo alocou em bytes durante a criação de perfil. Essa medida de memória virtual é conhecida como *bytes privados*. Os bytes privados representam os locais de memória virtual que foram alocados pelo processo que podem ser acessados somente por threads em execução no processo.|  
|[DA0506: máximo de bytes particulares alocados para o processo cujo perfil está sendo criado](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória virtual que o processo alocou em bytes privados durante a criação de perfil.|