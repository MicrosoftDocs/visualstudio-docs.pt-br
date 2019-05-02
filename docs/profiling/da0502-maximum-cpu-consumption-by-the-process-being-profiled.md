---
title: 'DA0502: Consumo máximo de CPU pelo processo do qual o perfil está sendo criado | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0502
- vs.performance.DA0502
- vs.performance.502
ms.assetid: 1ee53df5-b0dc-4265-9d4f-527830d08725
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7092e6424a5f00ed4461a91ed10bbf530597082
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935959"
---
# <a name="da0502-maximum-cpu-consumption-by-the-process-being-profiled"></a>DA0502: Consumo máximo de CPU pelo Processo cujo perfil está sendo criado

|||
|-|-|
|ID de regra|DA0502|
|Categoria|Monitoramento de recursos|
|Método de criação de perfil|Todos|
|Mensagem|Essa regra se destina apenas a fins informativos. O contador Processo()\\% de tempo do processador mede o consumo da CPU do processo do qual o perfil está sendo criado. O valor relatado é o máximo observado em todos os intervalos de medição.|
|Tipo de regra|Informativo|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="rule-description"></a>Descrição da regra
 Essa mensagem relata o percentual máximo de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é o valor máximo relatado entre todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo. O percentual pode ser maior que 100% em um computador com mais de um processador.

## <a name="how-to-use-the-rule-data"></a>Como usar os dados de regra
 Use o valor da regra para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de criação de perfil.