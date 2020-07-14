---
title: DA0501-consumo médio de CPU pelo processo que está sendo analisado. | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DA0501
- vs.performance.DA0501
- vs.performance.501
ms.assetid: b01946b4-75e3-47d5-a1a1-cebfae66a3af
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 7f03a65842664ec5d0ed2841f791dd168d82860e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544567"
---
# <a name="da0501-average-cpu-consumption-by-the-process-being-profiled"></a>DA0501: consumo médio da CPU pelo processo que está sendo analisado.

|Item|Valor|
|-|-|
|ID de regra|DA501|
|Categoria|Monitoramento de recursos|
|Método de criação de perfil|Todos|
|Mensagem|Consumo médio de CPU pelo Processo cujo perfil está sendo criado.|
|Tipo de regra|Informações|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="rule-description"></a>Descrição da regra
 Essa mensagem relata o percentual de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo. O valor do valor pode ser maior que 100% em um computador com mais de um processador.

## <a name="how-to-use-rule-data"></a>Como usar dados de regra
 Use o valor da regra para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de teste.
