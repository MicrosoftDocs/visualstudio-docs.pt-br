---
title: Usando várias ferramentas de criador de perfil simultaneamente | Microsoft Docs
ms.date: 4/29/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, multiple tools
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: f72757d46496c3990c0a0d4205753d185078eac7
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332043"
---
# <a name="using-multiple-profiler-tools-simultaneously"></a>Usando várias ferramentas de criador de perfil simultaneamente

O criador de perfil de desempenho foi projetado com a ideia de que várias ferramentas podem ser usadas na mesma sessão para ajudar a entender os problemas de desempenho. A maioria das ferramentas no criador de perfil de desempenho tem suporte em execução simultânea, como o [uso da CPU](../profiling/cpu-usage.md), a [ferramenta Async do .net](../profiling/analyze-async.md)e a ferramenta de [banco de dados](../profiling/analyze-database.md) . Para executar ferramentas simultaneamente na mesma sessão de diagnóstico, clique na caixa de seleção ao lado delas e inicie a sessão de diagnóstico.

![Todas as ferramentas selecionadas do hub de diagnóstico](../profiling/media/diaghuballtoolsselected.png "Todas as ferramentas selecionadas do hub de diagnóstico")

>[!NOTE]
>Determinadas ferramentas, como a ferramenta de [alocação de objeto .net](../profiling/dotnet-alloc-tool.md) , não podem ser executadas com outras ferramentas devido à alta sobrecarga ou devido a outras limitações técnicas.

## <a name="time-filtering"></a>Filtragem de tempo 

Durante a análise, as operações de filtragem de tempo são aplicadas em todas as ferramentas, para que você possa usar as informações em uma ferramenta para restringir um intervalo de tempo e filtrar dados em outra ferramenta. Esse recurso ajuda a analisar a análise para pontos específicos em um rastreamento e ajuda você a entender o estado do aplicativo.

![Filtragem de tempo do hub de diagnóstico](../profiling/media/diaghubtimefiltering.png "Filtragem de tempo do hub de diagnóstico")

## <a name="see-also"></a>Veja também

- [Otimizando as configurações do criador de perfil](../profiling/optimize-profiler-settings.md)
- [Executando ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [Entendendo sobre os métodos de coleta de desempenho](../profiling/understanding-performance-collection-methods-perf-profiler.md)
