---
title: Como escolher eventos de amostragem | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.sampling
helpviewer_keywords:
- clock cycles sample event
- sample events, choosing
- profiling tools, sample events
- page faults sample event
- system calls sample event
- performance counter sample event
- performance tools, sample events
ms.assetid: ce7cb734-80ac-4930-a4ef-e24395e1cc07
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8473ca1f5829faa2a76b5560132c7aada152dc3a
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329284"
---
# <a name="how-to-choose-sampling-events"></a>Como escolher eventos de amostragem
Por padrão, as ferramentas de criação de perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] coletam dados de desempenho em um intervalo especificado como um número de ciclos de processador que são usados pelo processo analisado. O número padrão de ciclos em um intervalo é de 10.000.000, que é aproximadamente 0,01 segundos em um computador de 1 GH. Você pode alterar o número de ciclos em um intervalo e também pode alterar o evento de amostragem. Os eventos de amostragem a seguir estão disponíveis:

- Ciclos do relógio – para problemas associados à CPU.

- Falhas de página – para problemas relacionados à memória.

- Chamadas do sistema – para problemas relacionados a E/S.

- Contador de desempenho – contadores de CPU para problemas de baixo desempenho.

> [!IMPORTANT]
> Se você estiver coletando dados de memória do .NET (alocações, tempos de vida do objeto ou ambos) usando o método de amostragem, todos os eventos de amostragem especificados pelo usuário serão ignorados e os eventos de alocação de memória ou de coleta de lixo adequados ou ambos, serão usados para coletar dados.

### <a name="to-select-a-sample-event"></a>Para selecionar um evento de amostragem

1. Em **Gerenciador de desempenho**, clique com o botão direito do mouse na sessão de desempenho e clique em **Propriedades**.

2. Nas **Páginas de Propriedades**, clique nas propriedades de **Amostragem**.

3. Na lista suspensa **Evento de amostra**, selecione o evento de amostragem que você deseja usar para criar o perfil de seu aplicativo.

    > [!NOTE]
    > Os **Contadores de desempenho disponíveis** serão habilitados somente se você selecionar **Contador de desempenho** na lista suspensa **Evento de amostra**.

4. Se você selecionar **Contador de desempenho**, selecione um contador de CPU específico no controle de exibição de árvore **Contadores de desempenho disponíveis**.

    - Os contadores no nó **Eventos Portáteis** estão disponíveis em todos os tipos de processadores.

    - Os contadores no nó **Eventos de Plataforma** são específicos para o processador no computador atual e podem não estar disponíveis em outros tipos de processadores.

5. Ao selecionar um evento de amostra, um valor de intervalo de amostragem padrão é exibido na caixa de texto **Intervalo de Amostragem**. Se necessário, insira o valor desejado na caixa de texto.

## <a name="see-also"></a>Veja também
- [Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)
- [Como: escolher métodos de coleção](../profiling/how-to-choose-collection-methods.md)
- [Contadores de CPU e do Windows](../profiling/cpu-and-windows-counters.md)
- [Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)
- [Criar perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)
