---
title: Como coletar dados do contador de CPU | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.cpucounters
helpviewer_keywords:
- profiling tools, using portable CPU counters
- performance tools, portable CPU counters
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c500316bd53ddce8bf731876e5963e6ef253bb27
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330917"
---
# <a name="how-to-collect-cpu-counter-data"></a>Como coletar dados do contador de CPU

Um contador de evento de CPU é usado para coletar dados de desempenho específicos de hardware. Este artigo mostra como coletar dados do contador de eventos quando você usa o método de criação de perfil de instrumentação.

Dois tipos de eventos do contador de CPU ocorrem:

- Eventos portáteis – eventos de CPU que podem ser coletados, independentemente da CPU específica.

- Eventos de plataforma – eventos de CPU que estão acoplados a uma CPU específica.

  Os eventos portáteis incluem eventos gerais, como Instruções Desativadas e Ciclos Não Interrompidos, eventos de buffer de CPU, eventos de ramificação e eventos de cache L2. Os contadores de evento de plataforma disponíveis são determinados pelo fabricante do processador.

  Categorias de eventos podem ser compartilhadas entre contadores de plataforma e portáteis. Por exemplo, as seguintes categorias de dados são frequentemente comuns aos dois tipos:

- Eventos de memória.

- Eventos de front-end.

- Eventos de ramificação.

  Colete dados do contador de desempenho de duas formas no criador de perfil:

- Colete dados de um ou mais contadores ao analisar por instrumentação.

- Especifique um evento de contador como o intervalo de amostragem, quando você analisar por amostragem. Para obter mais informações, consulte [como: escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md).

## <a name="to-collect-cpu-performance-counter-data-when-you-profile-by-instrumentation"></a>Para coletar dados de contador de desempenho de CPU ao analisar por instrumentação

1. Nas **Páginas de Propriedade** da sessão de desempenho, clique em **Contadores de CPU.**

2. Selecione a caixa de seleção **Coletar Contadores de CPU**.

3. Expanda a árvore **Contadores de desempenho disponíveis** até localizar os eventos de amostragem que você deseja coletar.

4. Para cada evento que você deseja coletar, selecione o evento e, em seguida, clique na seta à direita para adicionar o evento à lista de **Contadores Selecionados**.

    > [!NOTE]
    > **Contadores de desempenho disponíveis** estará habilitada somente se você selecionar a caixa de seleção **Coletar Contadores de CPU**.

## <a name="see-also"></a>Veja também

[Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho Propriedades da sessão de [desempenho](../profiling/performance-session-properties.md) 
 Contadores de CPU [e do Windows](../profiling/cpu-and-windows-counters.md) 
 [Como: escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md)
