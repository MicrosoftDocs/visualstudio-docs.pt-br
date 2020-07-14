---
title: Noções básicas sobre métodos de coleta de desempenho | Microsoft Docs
ms.date: 4/30/2020
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords:
- Performance Profiler, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2017'
ms.workload:
- multiple
ms.openlocfilehash: 03a49763a682f6b98b02fe40ba957efa8f5483c8
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290055"
---
# <a name="understand-performance-collection-methods"></a>Entender os métodos de coleta de desempenho

Este documento descreve os métodos de coleta de dados que as ferramentas do criador de perfil de desempenho do Visual Studio utilizam. 

## <a name="sampling"></a>amostragem

Os métodos de amostragem para a criação de perfil coletam dados estatísticos sobre o trabalho que é executado por um aplicativo durante uma execução de criação de perfil. A coleta de dados é feita coletando informações sobre o aplicativo em um intervalo regular ou uma frequência de amostragem, como a cada milissegundo e, em seguida, analisando esses dados para criar um modelo de onde o tempo foi gasto no aplicativo. O método de amostragem é leve e tem pouco efeito sobre a execução do aplicativo que está sendo criado para o perfil. As ferramentas no criador de perfil de desempenho que utilizam o método de amostragem incluem a ferramenta de [uso da CPU](../profiling/cpu-usage.md) .

## <a name="instrumentation"></a>Instrumentação

A criação de perfil de instrumentação coleta informações detalhadas sobre o trabalho que é executado por um aplicativo durante uma execução de criação de perfil. A coleta de dados é feita por ferramentas que inserem código em um arquivo binário que captura informações de tempo ou usando ganchos de retorno de chamada para coletar e emitir informações exatas de tempo e contagem de chamadas durante a execução de um aplicativo. O método de instrumentação tem uma alta sobrecarga quando comparado às abordagens baseadas em amostragem. As ferramentas no criador de perfil de desempenho que usam a instrumentação incluem a ferramenta de [alocação de objeto .net](../profiling/dotnet-alloc-tool.md) .