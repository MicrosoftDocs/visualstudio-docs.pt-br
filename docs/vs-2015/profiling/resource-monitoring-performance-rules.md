---
title: Regras de Desempenho do Monitoramento de Recurso | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 09c9e41061564a8ffb0e08e3aba75a0d4355d0d2
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54795389"
---
# <a name="resource-monitoring-performance-rules"></a>Regras de desempenho do monitoramento de recurso
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As mensagens de desempenho da categoria Monitoramento de Recurso fornecem dados adicionais sobre o desempenho do aplicativo. É possível utilizar esses dados para analisar problemas de desempenho. Essas regras são informativas e relatadas para todas as execuções de criação de perfil.  
  
|||  
|-|-|  
|[DA0501: Consumo médio de CPU pelo Processo cujo perfil está sendo criado.](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|  
|[DA0502: Consumo máximo de CPU pelo Processo cujo perfil está sendo criado](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual máximo de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é o valor máximo relatado entre todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|  
|[DA0503: Média de Conjunto de Trabalho em Bytes para o Processo cujo perfil está sendo criado](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória física em bytes que o processo usou enquanto a criação de perfil estava ativa. Essa medida de memória física é conhecida como conjunto de trabalho.|  
|[DA0504: Conjunto de Trabalho Máximo em Bytes para o Processo cujo perfil está sendo criado](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória física em bytes que o processo estava usando durante a criação de perfil.|  
|[DA0505: Média de Bytes Privados alocados para o Processo cujo perfil está sendo criado](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória virtual que o processo alocou em bytes durante a criação de perfil. Essa medida de memória virtual é conhecida como *bytes privados*. Os bytes privados representam os locais de memória virtual que foram alocados pelo processo que podem ser acessados somente por threads em execução no processo.|  
|[DA0506: Máximo de Bytes Privados alocados para o Processo cujo perfil está sendo criado](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória virtual que o processo alocou em bytes privados durante a criação de perfil.|
