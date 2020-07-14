---
title: Compreendendo os métodos de coleta de desempenho | Microsoft Docs
ms.date: 4/30/2020
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.methodpage
helpviewer_keywords:
- Profiling tools, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 0a37d58d1bd18ef19f610602ec8f2238816405e4
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285745"
---
# <a name="understand-performance-collection-methods"></a>Entender os métodos de coleta de desempenho

As ferramentas de criação de perfil do Visual Studio fornecem cinco métodos para coletar dados de desempenho. Este artigo descreve os diferentes métodos e sugere cenários nos quais a coleta de dados com um método específico pode ser apropriada.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiam alterações significativas na forma como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

|Método|Descrição|
|------------|-----------------|
|[Amostragem](#sampling)|Coleta dados estatísticos sobre o trabalho feito por um aplicativo.|
|[Instrumentação](#instrumentation)|Coleta informações de tempo detalhados sobre cada chamada de função.|
|[Simultaneidade](#concurrency)|Coleta informações detalhadas sobre aplicativos multissegmentados.|
|[Memória do .NET](#net-memory)|Coleta informações detalhadas sobre coleta de lixo e de alocação de memória do .NET.|
|[Interação entre camadas](#tier-interaction)|Coleta informações sobre chamadas de função ADO.NET síncronas para um banco de dados SQL Server.<br /><br /> Qualquer edição do Visual Studio pode coletar dados de perfil de interação de camada. No entanto, você pode exibir esses dados somente em Visual Studio Enterprise.|

Ao usar alguns dos métodos de criação de perfil, você também pode coletar dados adicionais, como contadores de desempenho de software e hardware. Para obter mais informações, confira [Coletar dados de desempenho adicionais](../profiling/collecting-additional-performance-data.md).

## <a name="sampling"></a>amostragem

O método de criação de perfil de amostragem coleta dados estatísticos sobre o trabalho que um aplicativo faz durante uma execução de criação de perfil. O método de amostragem é leve e tem pouco efeito na execução de métodos de aplicativo.

A amostragem é o método padrão das ferramentas de criação de perfil do Visual Studio. Ele é útil para as seguintes tarefas:

- Explorações iniciais do desempenho do seu aplicativo
- Investigando problemas de desempenho que envolvem a utilização do microprocessador (CPU)

O método de criação de perfil de amostragem interrompe a CPU do computador em intervalos definidos e coleta a pilha de chamadas de função. As contagens de amostra exclusivas são incrementadas para a função que está em execução. As contagens inclusivas são incrementadas para todas as funções de chamada na pilha de chamadas. Os relatórios de amostragem apresentam os totais dessas contagens para os módulos com perfil, funções, linhas de código-fonte e instruções.

Por padrão, o criador de perfil define o intervalo de amostragem para ciclos de CPU. Você pode alterar o tipo de intervalo para outro contador de desempenho de CPU ou definir o número de eventos de contador para o intervalo. Você também pode coletar dados de criação de perfil de interação de camada (TIP). Esses dados fornecem informações sobre as consultas feitas a um banco de dado SQL Server por meio de ADO.NET.

[Coletar estatísticas de desempenho usando amostragem](../profiling/collecting-performance-statistics-by-using-sampling.md)

[Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)

[Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)

## <a name="instrumentation"></a>Instrumentação

O método de criação de perfil de instrumentação coleta o tempo detalhado das chamadas de função em um aplicativo de perfil. A criação de perfil de instrumentação é útil para estas tarefas:

- Investigando afunilamentos de entrada/saída, como e/s de disco
- Fechar o exame de um módulo específico ou de um conjunto de funções

O método de instrumentação injeta o código em um arquivo binário. O código captura informações de tempo para todas as funções no arquivo instrumentado e cada chamada de função feita por essas funções. A instrumentação também identifica quando uma função chama o sistema operacional para operações como gravar em um arquivo.

Os relatórios de instrumentação usam esses quatro valores para representar o tempo total gasto em uma função ou linha de código-fonte:

- Inclusão decorrida – o tempo total gasto na execução da função ou linha de código-fonte.

- Aplicativo inclusivo – o tempo gasto na execução da função ou linha de código-fonte. As chamadas para o sistema operacional são excluídas.

- Decorrido exclusivo – o tempo gasto na execução da função ou linha de código-fonte. Chamadas para outras funções são excluídas.

- Aplicativo exclusivo – o tempo gasto na execução da função ou linha de código-fonte. Chamadas para o sistema operacional ou outras funções são excluídas.

Você também pode coletar contadores de desempenho de CPU e software usando o método de instrumentação.

[Noções básicas sobre valores de dados de instrumentação](../profiling/understanding-instrumentation-data-values.md)

[Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)

[Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)

## <a name="concurrency"></a>Simultaneidade

A criação de perfil de simultaneidade coleta informações sobre aplicativos multissegmentados. A criação de perfil de contenção de recursos coleta informações detalhadas da pilha de chamadas sempre que os threads concorrentes aguardam o acesso a um recurso compartilhado. A visualização de simultaneidade também coleta informações mais gerais sobre como seu aplicativo multithread interage com:

  - Próprio.
  - O hardware.
  - O sistema operacional.
  - Outros processos no computador host.

Relatórios de contenção de recursos exibem o número total de contenções. Eles também relatam o tempo total que os módulos, as funções, as linhas de código-fonte e as instruções aguardaram por um recurso. Os gráficos de linha do tempo mostram as contenções que ocorreram.

O Visualizador de simultaneidade exibe informações gráficas para ajudá-lo a localizar:

  - Afunilamentos de desempenho.
  - Subutilização da CPU.
  - Contenção de thread.
  - Migração de threads.
  - Atrasos de sincronização.
  - Áreas de e/s sobrepostas.

  Quando possível, a saída gráfica é vinculada aos dados da pilha de chamadas e do código-fonte. Os dados de visualização de simultaneidade podem ser coletados somente para aplicativos de linha de comando e aplicativos do Windows.

[Noções básicas sobre valores de dados de contenção de recurso](../profiling/understanding-resource-contention-data-values.md)

[Coletar dados de simultaneidade de thread e do processo](../profiling/collecting-thread-and-process-concurrency-data.md)

[Exibições de dados de contenção de recursos](../profiling/resource-contention-data-views.md)

[Visualizador de Simultaneidade](../profiling/concurrency-visualizer.md)

## <a name="net-memory"></a>Memória do .NET

O método de criação de perfil para a alocação de memória do .NET interrompe a CPU em cada alocação de um objeto .NET Framework em um aplicativo de perfil. Quando o criador de perfil também coleta dados de tempo de vida do objeto, ele interrompe a CPU após cada .NET Framework coleta de lixo.

O criador de perfil coleta informações sobre o tipo, o tamanho e o número de objetos criados em uma alocação ou destruídos na coleta de lixo.

- Quando ocorre um evento de alocação, o criador de perfil coleta informações adicionais sobre a pilha de chamadas de função. O criador de perfil incrementa as contagens de alocação exclusivas para a função em execução no momento. Ele também incrementa as contagens inclusivas para todas as funções de chamada na pilha de chamadas. Os relatórios do .NET apresentam os totais dessas contagens para os tipos de perfil, módulos, funções, linhas de código-fonte e instruções.

- Quando ocorre a coleta de lixo, o criador de perfil coleta dados sobre os objetos destruídos e sobre os objetos em cada geração de coleta de lixo. No final da execução da criação de perfil, o criador de perfil registra dados sobre os objetos que não foram explicitamente destruídos. O relatório tempo de vida do objeto exibe os totais de cada tipo alocado na execução da criação de perfil.

Você pode usar a criação de perfil de memória do .NET no modo de amostragem ou no modo de instrumentação. O modo selecionado não afeta os relatórios de alocação e de tempo de vida do objeto que são exclusivos da criação de perfil de memória do .NET.

- Quando você executa a criação de perfil de memória do .NET no modo de amostragem, o criador de perfil usa eventos de alocação de memória como o intervalo. Ele também exibe o número total de objetos e bytes alocados como os valores inclusivos e exclusivos nos relatórios.

- Quando você executa a criação de perfil de memória do .NET no modo de instrumentação, o criador de perfil coleta informações detalhadas de tempo junto com os valores de alocação inclusivos e exclusivos.

[Entender a alocação de memória e os valores de dados de tempo de vida do objeto](../profiling/understanding-memory-allocation-and-object-lifetime-data-values.md)

[Coletar dados de tempo de vida e de alocação de memória do .NET](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

[Exibições de dados de memória do .NET](../profiling/dotnet-memory-data-views.md)

## <a name="tier-interaction"></a>Interação entre camadas

A criação de perfil de interação de camada adiciona informações a um arquivo de dados de criação de perfil sobre chamadas síncronas [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] entre uma [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] página ou outro aplicativo e um banco de dado [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] . Os dados incluem o número e a hora de chamadas e o tempo máximo e mínimo. Você pode adicionar dados de interação de camada a dados de criação de perfil coletados com os métodos de amostragem, instrumentação, memória .NET ou simultaneidade.

![Fluxo de transmissão de criação de perfil de interação de camada](../profiling/media/tierinteraction_profilingtools.png "Fluxo de transmissão de criação de perfil de interação de camada")

Para obter informações sobre dados de interação de camada coletados por ferramentas de criação de perfil, consulte os artigos a seguir.

[Coletar dados de interação de camada](../profiling/collecting-tier-interaction-data.md)

[Modos de exibição de interação de camada](../profiling/tier-interaction-views.md)

## <a name="see-also"></a>Veja também

[Como coletar dados de desempenho de um site](../profiling/how-to-collect-performance-data-for-a-web-site.md)

[Guia para iniciantes para criação de perfil de desempenho](../profiling/beginners-guide-to-performance-profiling.md)
