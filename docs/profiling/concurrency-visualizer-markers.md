---
title: Marcadores da Visualização Simultânea | Microsoft Docs
description: 'Saiba mais sobre marcadores no Visualizador de simultaneidade. Os marcadores são ícones que representam eventos gerados por um aplicativo. Há três tipos: sinalizadores, mensagens e intervalos.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.markersui
ms.assetid: c4692d17-6cd2-4ad1-8590-d7275c771c70
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fab8108e15f3cbaf81130c2ce8533d00f2a23c7e
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720989"
---
# <a name="concurrency-visualizer-markers"></a>Marcadores da Visualização Simultânea
Na Visualização Simultânea, os marcadores são ícones que representam os eventos em um aplicativo.  Normalmente, o aplicativo gera esses eventos para designar fases ou ocorrências em um aplicativo.  Os eventos podem ser gerados pelo aplicativo ou por bibliotecas e runtimes que o aplicativo usa.

## <a name="kinds-of-markers"></a>Tipos de marcadores
 A Visualização Simultânea usa três tipos de marcadores para representar eventos do aplicativo: sinalizadores, mensagens e intervalos.

1. Use um *sinalizador* para indicar um ponto no tempo interessante em seu aplicativo.  Por exemplo, é possível usar um sinalizador para representar que o valor de uma variável atingiu um certo limite ou que uma exceção foi lançada.

2. Uma *mensagem* também marca um ponto no tempo, mas é possível usá-la para rastreamento de estilo do log.  Por exemplo, o que pode ter sido despejado em um arquivo de log agora pode ser encapsulado em uma chamada de mensagem para poder rastreá-la e visualizá-la na Visualização Simultânea. Também é possível usar a Visualização Simultânea para exportar esses dados para um arquivo CSV.

3. O *intervalo* representa um intervalo de tempo em seu aplicativo, por exemplo, uma das suas fases.

## <a name="marker-linkage-to-threads"></a>Vinculação de marcador para threads
 Cada thread que gera marcadores tem um canal separado de linha do tempo.  A ID do thread responsável por gerar os eventos de marcador é mostrada ao lado da descrição do canal do marcador.  A ID mostrada no lado esquerdo do canal do marcador corresponde à ID de outro thread no processo atual.

## <a name="marker-importance"></a>Importância do marcador
 Os marcadores podem ter um dos quatro níveis de importância: baixa, normal, alta e crítica.  É possível filtrar as fontes de marcadores com base no nível de importância.  Por exemplo, se você só desejar ver os marcadores de uma fonte específica que tem importância normal ou crítica, será possível configurar o filtro na caixa de diálogo [Configurações avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md). A importância de um marcador é exibida em sua dica de ferramenta e no [Relatório de Marcadores](../profiling/markers-report.md).

## <a name="marker-category"></a>Categoria de marcador
 Uma categoria de marcador indica um grupo de eventos de marcador que vêm da mesma fonte.  A Visualização Simultânea usa cor para diferenciar diferentes categorias de sinalizadores e intervalos. É possível configurar a Visualização Simultânea para usar categorias para filtrar os eventos de marcador em um provedor de eventos específico.  Use a caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) para configurar o filtro.

## <a name="known-sources-of-markers"></a>Fontes conhecidas de marcadores
 Qualquer provedor ETW pode gerar marcadores, desde que os provedores obedeçam a determinadas restrições. É possível configurar a Visualização Simultânea para escutar outras fontes de evento para marcadores. Por padrão, ele escuta estas fontes de evento:

- [SDK do Visualizador de Simultaneidade](../profiling/concurrency-visualizer-sdk.md)

- [Biblioteca de tarefas paralelas (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)

- [Fluxo de dados](/dotnet/standard/parallel-programming/dataflow-task-parallel-library)

- [LINQ paralelo (PLINQ)](/dotnet/standard/parallel-programming/parallel-linq-plinq)

- [Runtime de Simultaneidade](/cpp/parallel/concrt/concurrency-runtime)

- [Suporte do Marcador de Cenário](/previous-versions/visualstudio/visual-studio-2010/dd984115\(v\=vs.100\))

- [C++ AMP (C++ Accelerated Massive Parallelism)](/cpp/parallel/amp/cpp-amp-cpp-accelerated-massive-parallelism)

  É possível usar a guia Marcadores na caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) para controlar se os marcadores de várias fontes são exibidos na Visualização Simultânea e é possível filtrá-los com base na importância e na categoria.

## <a name="markers-from-eventsource"></a>Marcadores de EventSource
 A Visualização Simultânea também pode exibir eventos EventSource.  Para obter mais informações, confira [Visualizar eventos EventSource como marcadores](../profiling/visualizing-eventsource-events-as-markers.md).

## <a name="see-also"></a>Confira também
- [Marcadores de sinalizador](../profiling/flag-markers.md)
- [Marcadores de mensagem](../profiling/message-markers.md)
- [Marcadores de span](../profiling/span-markers.md)
- [Visualizar eventos EventSource como marcadores](../profiling/visualizing-eventsource-events-as-markers.md)