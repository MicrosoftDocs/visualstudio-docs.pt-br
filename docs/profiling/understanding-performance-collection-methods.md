---
title: Noções básicas sobre métodos de coleta de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.methodpage
helpviewer_keywords:
- Profiling Tools, profiling methods
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d278f8ca6019dd8a29d5e4c57e1e191137a32972
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668116"
---
# <a name="understand-performance-collection-methods"></a>Entender os métodos de coleta de desempenho

As ferramentas de Perfil do Visual Studio fornecem cinco métodos que você pode usar para coletar dados de desempenho. Este tópico descreve os diferentes métodos e sugere alguns cenários nos quais a coleta de dados com um método específico pode ser apropriada.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

|Método|Descrição|
|------------|-----------------|
|[Amostragem](#sampling)|Coleta dados estatísticos sobre o trabalho executado por um aplicativo.|
|[Instrumentação](#instrumentation)|Coleta informações de tempo detalhados sobre cada chamada de função.|
|[Simultaneidade](#concurrency)|Coleta informações detalhadas sobre aplicativos multithread.|
|[Memória do .NET](#net-memory)|Coleta informações detalhadas sobre coleta de lixo e de alocação de memória do .NET.|
|[Interações de Camada](#tier-interaction)|Coleta informações sobre chamadas de função ADO.NET síncronas para um banco de dados do SQL Server.<br /><br /> A criação de perfil de interação de camadas pode ser coletada usando qualquer edição do Visual Studio. No entanto, os dados de criação de perfil de interação de camadas só podem ser exibidos no Visual Studio Enterprise.|

Usando alguns dos métodos de criação de perfil, você também pode coletar dados adicionais, como contadores de desempenho de software e hardware. Para obter mais informações, confira [Coletar dados de desempenho adicionais](../profiling/collecting-additional-performance-data.md).

## <a name="sampling"></a>Amostragem

O método de criação de perfil de amostragem coleta dados estatísticos sobre o trabalho executado por um aplicativo durante uma execução de criação de perfil. O método de amostragem é simples e tem pouco efeito na execução dos métodos de aplicativo.

A amostragem é o método padrão de ferramentas de criação de perfil do Visual Studio. É útil para o seguinte:

- Explorações inicias do desempenho de seu aplicativo.
- Investigar problemas de desempenho que envolvem a utilização do processador (CPU).

O método de criação de perfil de amostragem interrompe o processador do computador em intervalos definidos e coleta a pilha de chamadas de função. Contagens exclusivas de exemplo são incrementadas para a função que está em execução e contagens inclusivas são incrementadas para todas as funções de chamada na pilha de chamadas. Relatórios de amostragem apresentam os totais dessas contagens para o módulo com perfil, função, linha de código-fonte e instruções.

Por padrão, o criador de perfil define o intervalo de amostragem para ciclos de CPU. Você pode alterar o tipo de intervalo para outro contador de desempenho de CPU e você pode definir o número de eventos do contador para o intervalo. Você também pode coletar dados de perfil (TIP) de interação de camadas que fornece informações sobre as consultas feitas em um banco de dados do SQL Server por meio do ADO.NET.

[Coletar estatísticas de desempenho usando amostragem](../profiling/collecting-performance-statistics-by-using-sampling.md)

[Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)

[Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)

## <a name="instrumentation"></a>Instrumentação

A método de criação de perfil de instrumentação coleta tempo detalhado para as chamadas de função em um aplicativo de perfil. Criação de perfil de instrumentação é útil para o seguinte:

- Investigar gargalos de entrada/saída, como E/S de disco.
- Exame detalhado de um módulo específico ou conjunto de funções.

O método de instrumentação injeta código em um arquivo binário que captura as informações de tempo para cada função no arquivo instrumentado e cada chamada de função feita por essas funções. Instrumentação também identifica quando uma função chama a operação para operações, como gravar em um arquivo. Relatórios de instrumentação usam quatro valores para representar o tempo total gasto em uma linha de código-fonte ou de função:

- Tempo Inclusivo decorrido – o tempo total gasto para executar a linha de origem ou de função.

- Aplicativo inclusivo – o tempo gasto para executar a função ou fonte de linha, mas excluindo o tempo gasto em chamadas para o sistema operacional.

- Exclusivo decorrido – o tempo gasto executando código no corpo da função ou linha de código-fonte. Tempo gasto executando funções que são chamadas pela função ou linha de origem é excluído.

- Exclusivo de aplicativo – o tempo gasto executando código no corpo da função ou linha de código-fonte. Tempo gasto executando chamadas para o sistema operacional e o tempo gasto executando funções que são chamadas pela função ou linha de origem é excluída.

Você também pode coletar contadores de desempenho da CPU e de software usando o método de instrumentação.

[Entender os valores de dados de instrumentação](../profiling/understanding-instrumentation-data-values.md)

[Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)

[Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)

## <a name="concurrency"></a>Concorrência

Criação de perfil de simultaneidade coleta informações sobre aplicativos multithread. Contenção de recursos perfis coleta informações de pilha de chamadas detalhada toda vez que threads simultâneas são forçadas a aguardar o acesso a um recurso compartilhado. Visualização de simultaneidade também coleta informações mais gerais sobre como seu aplicativo multithread interage consigo mesmo, o hardware, o sistema operacional e outros processos no computador host:

- Relatórios de contenção do recurso exibem o número total de contenções e o tempo total gasto aguardando um recurso para os módulos, funções, linhas de código-fonte e instruções no qual ocorreu a espera. Gráficos de linha do tempo também mostram a contenção, conforme ocorreram.

- A Visualização Simultânea exibe informações gráficas que você pode usar para localizar o gargalo de desempenho, subutilização da CPU, contenção de thread, migração de thread, atrasos de sincronização, áreas de E/S sobrepostas e outras informações. Quando possível, os links de saída gráfica para a pilha de chamadas e os dados de código-fonte. Dados de visualização de simultaneidade podem ser coletados apenas para linha de comando e aplicativos do Windows.

[Entender os valores de dados de contenção de recursos](../profiling/understanding-resource-contention-data-values.md)

[Coletar dados de simultaneidade do thread e do processo](../profiling/collecting-thread-and-process-concurrency-data.md)

[Exibições de dados da contenção de recurso](../profiling/resource-contention-data-views.md)

[Visualização Simultânea](../profiling/concurrency-visualizer.md)

## <a name="net-memory"></a>Memória do .NET

O método de criação de perfil para alocação de memória do .NET interrompe o processador do computador em cada alocação de um objeto do .NET Framework em um aplicativo de perfil. Quando os dados de tempo de vida do objeto também são coletados, o criador de perfil interrompe o processador após cada coleta de lixo do .NET Framework.

O criador de perfil coleta informações sobre o tipo, tamanho e número de objetos que foram criados em uma alocação ou foram destruídos em uma coleta de lixo.

- Quando ocorre um evento de alocação, o criador de perfil coleta informações adicionais sobre a pilha de chamadas de função. Contagens de alocações exclusivas são incrementadas para a função que está sendo executada, contagens inclusivas são incrementadas para todas as funções de chamada na pilha de chamadas. Relatórios de .NET apresentam os totais dessas contagens de tipos de perfil, módulos, funções, linhas de código-fonte e instruções.

- Quando ocorre uma coleta de lixo, o criador de perfil coleta dados sobre os objetos que foram destruídos e informações sobre os objetos em cada geração de coleta de lixo. No final da criação de perfil, o criador de perfil registra dados sobre os objetos que não foram explicitamente destruídos. O relatório de tempo de vida do objeto exibe os totais para cada tipo que foi alocado na execução de criação de perfil.

O perfil de memória do .NET pode ser usado no modo de amostragem ou instrumentação. O modo que você seleciona não afeta a alocação e tempo de vida do objeto relata que é exclusivo do perfil de memória do .NET:

- Quando você executa os perfis de memória do .NET no modo de amostragem, o criador de perfil .NET usa eventos de alocação de memória como o intervalo e exibe o número de objetos que foram alocados e o total de bytes que foram alocados como os valores exclusivos e inclusivos nos relatórios.

- Quando você executa a criação de perfil da memória do .NET no modo de instrumentação, são coletadas informações de tempo detalhadas junto com os valores de alocação inclusivas e exclusivas.

[Entender a alocação de memória e os valores de dados de tempo de vida do objeto](../profiling/understanding-memory-allocation-and-object-lifetime-data-values.md)

[Coletar a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

[Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)

## <a name="tier-interaction"></a>Interação entre camadas

Criação de perfil de interação de camadas adiciona informações a um arquivo de dados de criação de perfil sobre chamadas [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] síncronas entre uma [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] página ou em outro aplicativo e um [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] banco de dados. Os dados incluem o número e a hora de chamadas e os tempos mínimos e máximos. Dados de interação de camadas podem ser adicionados para criação de perfil de dados que são coletados com a amostragem, instrumentação, memória do .NET ou métodos de simultaneidade.

![Dados de perfil da interação entre camadas](../profiling/media/tierinteraction_profilingtools.png "TierInteraction_ProfilingTools")

Dados de interação de camadas que são coletados por ferramentas de criação de perfil

[Coletar dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)

[Exibições de interação entre camadas](../profiling/tier-interaction-views.md)

## <a name="see-also"></a>Consulte também

[Como coletar dados de desempenho de um site](../profiling/how-to-collect-performance-data-for-a-web-site.md)  
[Guia do iniciante à criação de perfil de desempenho](../profiling/beginners-guide-to-performance-profiling.md)