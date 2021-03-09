---
title: DA0004-alto uso do processador | Microsoft Docs
description: A utilização do processador (CPU) estava alta em dados de criação de perfil que foram coletados usando o método de instrumentação.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAHighProcessorUsage
- vs.performance.rules.DA0004
- vs.performance.DA0004
- vs.performance.4
ms.assetid: 2c4fb569-929e-4f1d-8c50-b590ee371351
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e80f9161e435a3b2b615aed700714a0c3cd0efa4
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469969"
---
# <a name="da0004-high-processor-usage"></a>DA0004: Uso do processador elevado

|Item|Valor|
|-|-|
|ID de regra|DA0004|
|Categoria|Uso das ferramentas de criação de perfil|
|Métodos de criação de perfil|Instrumentação<br /><br /> amostragem|
|Mensagem|O uso do processador é consistentemente superior a 75%. Considere o uso do modo de Amostragem para aplicativos associados à CPU.|
|Tipo de regra|Informações|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="cause"></a>Causa
 A utilização do processador (CPU) estava alta em dados de criação de perfil que foram coletados usando o método de instrumentação. Considere o uso do método de criação de perfil de amostragem ao criar o perfil de um aplicativo associado à CPU.

## <a name="rule-description"></a>Descrição da regra
 Durante essa execução de criação de perfil, o processador (ou os processadores) estava consistentemente ocupado. A alta utilização da CPU pode indicar um aplicativo associado à CPU. Perfis instrumentados não são a maneira mais eficiente de investigar cenários de uso da CPU. A amostragem é mais eficaz quando você está criando o perfil de aplicativos que gastam muito tempo para executar instruções no processador.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Considere uma nova criação de perfil do aplicativo usando o método de amostragem em vez do método de instrumentação, a menos que você precise de tempos de função ou esteja mais interessado em entender a entrada/saída do que os gargalos do processador.
