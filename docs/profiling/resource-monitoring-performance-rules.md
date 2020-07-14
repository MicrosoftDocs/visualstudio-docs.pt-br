---
title: Regras de Desempenho do Monitoramento de Recurso | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 39df18811a47dfb41c17333121cd9a23d8f46940
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544528"
---
# <a name="resource-monitoring-performance-rules"></a>Regras de desempenho do monitoramento de recurso
As mensagens de desempenho da categoria Monitoramento de Recurso fornecem dados adicionais sobre o desempenho do aplicativo. É possível utilizar esses dados para analisar problemas de desempenho. Essas regras são informativas e relatadas para todas as execuções de criação de perfil.

|Regra|Descrição|
|-|-|
|[DA0501: consumo médio de CPU pelo processo que está sendo analisado.](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|
|[DA0502: Consumo máximo de CPU pelo Processo cujo perfil está sendo criado](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|Essa mensagem relata o percentual máximo de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é o valor máximo relatado entre todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.|
|[DA0503: Média de Conjunto de Trabalho em Bytes para o Processo cujo perfil está sendo criado](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória física em bytes que o processo usou enquanto a criação de perfil estava ativa. Essa medida de memória física é conhecida como conjunto de trabalho.|
|[DA0504: Conjunto de trabalho máximo em bytes para o processo cujo perfil está sendo criado](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória física em bytes que o processo estava usando durante a criação de perfil.|
|[DA0505: Média de Bytes Privados alocados para o Processo cujo perfil está sendo criado](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade média de memória virtual que o processo alocou em bytes durante a criação de perfil. Essa medida de memória virtual é conhecida como *bytes privados*. Os bytes privados representam os locais de memória virtual que foram alocados pelo processo que podem ser acessados somente por threads em execução no processo.|
|[DA0506: Máximo de Bytes Privados alocados para o Processo cujo perfil está sendo criado](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|Essa mensagem relata a quantidade máxima de memória virtual que o processo alocou em bytes privados durante a criação de perfil.|
