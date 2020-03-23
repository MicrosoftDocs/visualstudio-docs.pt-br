---
title: Exibição Resumo – Dados de amostragem | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method, Summary view
- Summary view
ms.assetid: 79056873-2985-40be-9112-cdbc26a65156
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 649d0e9e5b32c124cfa962f45e4d128e4a32210f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778200"
---
# <a name="summary-view---sampling-data"></a>Exibição Resumo – dados de amostragem
A exibição Resumo exibe informações sobre as funções mais caras de desempenho em uma execução da criação de perfil. Para obter mais informações, incluindo uma descrição das listas Links de notificação e Relatório, consulte [Exibição Resumo](../profiling/summary-view.md).

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## <a name="timeline-graph"></a>Gráfico de linha do tempo
 O gráfico de linha do tempo na exibição Resumo mostra o percentual da utilização do processador (CPU) do aplicativo com perfil ao longo do tempo em que ocorreu a criação de perfil. É possível usar o gráfico de linha do tempo para filtrar a exibição para um intervalo de tempo selecionado. Para obter mais informações, consulte [Como: Filtrar as visualizações do relatório da linha do tempo de resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md).

## <a name="hot-path"></a>Afunilamento
 O **Afunilamento** exibe o caminho de execução no qual a maioria das amostras foi coletada. É possível clicar em uma função para mostrar a exibição Detalhes da Função referente a ela. Para exibir outras exibições da função, clique com o botão direito do mouse na função e, em seguida, clique em uma exibição na lista.

 O **Afunilamento** inclui os seguintes dados para cada função:

|Coluna|Descrição|
|------------|-----------------|
|**Nome**|O nome da função.|
|**% de Amostras Inclusivas**|O percentual de todas as amostras que ocorreram quando essa função ou uma função chamada por essa função estava em execução.|
|**% de Amostras Exclusivas**|O percentual de todas as amostras que ocorreram durante a execução de código pela função em seu corpo. As amostras coletadas em funções chamadas por essa função não são incluídas.|

## <a name="functions-doing-most-individual-work"></a>Funções Que Realizam a Maioria do Trabalho Individual
 A lista **Funções que realizam a maior parte do trabalho individual** exibe as funções que têm o maior número de amostras exclusivas na execução de criação de perfil. Uma amostra exclusiva é atribuída a uma função se a função está executando seu próprio código quando a amostra foi coletada. Uma amostra exclusiva não é atribuída a uma função se a função está chamando outra função quando a amostra foi coletada. Um grande número de amostras exclusivas indica que um tempo significativo foi gasto na própria função.

 É possível clicar em uma função para mostrar a exibição Detalhes da Função referente a ela. Para exibir outras exibições da função, clique com o botão direito do mouse na função e, em seguida, clique em uma exibição na lista.

 **Funções que realizam a maior parte do trabalho individual** inclui os seguintes dados para cada função:

|Coluna|Descrição|
|------------|-----------------|
|**Nome**|O nome da função.|
|**% de Amostras Exclusivas**|O percentual de todas as amostras na execução de criação de perfil coletadas durante a execução de código pela função em seu corpo. O percentual exclui as amostras que foram coletadas quando as funções chamadas por essa função estavam em execução.|

## <a name="see-also"></a>Confira também
- [Resumo Exibição - Dados de memória .NET](../profiling/summary-view-dotnet-memory-data.md)
- [Resumo - dados de instrumentação](../profiling/summary-view-instrumentation-data.md)
