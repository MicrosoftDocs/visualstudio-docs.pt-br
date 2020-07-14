---
title: DA0008-poucos exemplos coletados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DATooFewSamples
- vs.performance.8
- vs.performance.DA0008
- vs.performance.rules.DA0008
ms.assetid: 8a5b78aa-7b3d-476c-a47d-abfaff3fae7c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5dd1114f4be0ed943c9a582c04d9917b03ca75c3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520777"
---
# <a name="da0008-few-samples-collected"></a>DA0008: Poucas amostras coletadas

|Item|Valor|
|-|-|
|ID de regra|DA0008|
|Categoria|Uso das ferramentas de criação de perfil|
|Método de criação de perfil|amostragem|
|Mensagem|Apenas algumas amostras foram coletadas. Considere uma execução mais longa ou uma taxa de amostragem mais rápida para obter resultados mais significativos.|
|Tipo de regra|Informações|

## <a name="cause"></a>Causa
 Apenas algumas amostras foram coletadas na execução de criação de perfil.

## <a name="rule-description"></a>Descrição da regra
 Quando o método de amostragem é usado, é necessário coletar um número estatisticamente significativo de amostras para ter certeza de que os dados representam o comportamento real do programa. Para minimizar os erros de amostragem, é necessário tentar coletar, no mínimo, 1.000 amostras de comportamento de execução de instrução do programa. Se você não coletar amostras suficientes, poderá se confundir ao analisar os dados de criação de perfil.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Considere a criação de perfil de uma execução mais longa do aplicativo ou o uso de uma taxa de amostragem mais rápida para obter resultados estatisticamente significativos. Para obter informações sobre como alterar a taxa de amostragem no IDE do Visual Studio, consulte [como: escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md). Para obter mais informações sobre como alterar a taxa de amostragem ao usar a linha de comando das Ferramentas de Criação de Perfil, consulte [Timer](../profiling/timer.md) na referência [VSPerfCmd](../profiling/vsperfcmd.md).
