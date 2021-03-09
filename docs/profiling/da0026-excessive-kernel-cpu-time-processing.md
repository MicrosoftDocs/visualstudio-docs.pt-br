---
title: DA0026-processamento excessivo de tempo de CPU do kernel | Microsoft Docs
description: A proporção de tempo da CPU que foi executada em modo kernel excedeu o tempo gasto no modo de usuário.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DA0026
- vs.performance.DA0026
- vs.performance.26
ms.assetid: 4cfc8a29-b29b-4a72-b386-03d8856fdf8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d39318433194693ee2b2cbbc8a94753cf2acd75d
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102465862"
---
# <a name="da0026-excessive-kernel-cpu-time-processing"></a>DA0026: Processamento de tempo de CPU do kernel excessivo

|Item|Valor|
|-|-|
|ID de regra|TODO|
|Categoria|Uso das ferramentas de criação de perfil|
|Método de criação de perfil|amostragem|
|Mensagem|Uma quantidade relativamente alta de tempo da CPU do modo kernel foi medida. Considere a investigação da fonte com a amostragem de SysCall habilitada.|
|Tipo de regra|Informações|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="cause"></a>Causa
 A proporção de tempo da CPU que foi executada em modo kernel excedeu o tempo gasto no modo de usuário. Considere uma nova criação de perfil e a amostragem do número de chamadas do sistema (syscalls) para determinar a causa dos altos tempos de execução de modo do kernel.

## <a name="rule-description"></a>Descrição da regra
 A proporção relativamente alta de tempo gasto pelo aplicativo na execução em modo kernel pode garantir uma investigação adicional. Um aplicativo de modo de usuário faz a transição para o modo de kernel para executar operações de E/S, aguardar os primitivos de sincronização de thread ou de processo ou fazer chamadas do sistema. É possível investigar os tipos de chamadas do sistema feitas pelo aplicativo e quais funções são responsáveis por elas ao selecionar a opção para coletar as pilhas de chamadas de amostra com base em chamadas do Sistema.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para investigar os tipos de chamadas do sistema feitas pelo aplicativo, execute o perfil novamente e selecione a opção para coletar amostras com base em chamadas do sistema. Consulte [Como escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md) se estiver executando as ferramentas de criação de perfil na IDE para obter mais informações. Se você estiver executando as ferramentas de criação de perfil por meio da linha de comando, confira a seção **Opções de intervalo de exemplo** do artigo [VSPerfCmd](../profiling/vsperfcmd.md) na referência das ferramentas de linha de comando das Ferramentas de Criação de Perfil.
