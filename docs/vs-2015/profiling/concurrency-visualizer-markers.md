---
title: Marcadores da Visualização Simultânea | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.cv.markersui
ms.assetid: c4692d17-6cd2-4ad1-8590-d7275c771c70
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4fa2a57d08f2b86fec573f02129a326907e3e3a9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790442"
---
# <a name="concurrency-visualizer-markers"></a>Marcadores do Visualizador de Simultaneidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na Visualização Simultânea, os marcadores são ícones que representam os eventos em um aplicativo.  Normalmente, o aplicativo gera esses eventos para designar fases ou ocorrências em um aplicativo.  Os eventos podem ser gerados pelo aplicativo ou por bibliotecas e tempos de execução que o aplicativo usa.  
  
## <a name="kinds-of-markers"></a>Tipos de marcadores  
 A Visualização Simultânea usa três tipos de marcadores para representar eventos do aplicativo: sinalizadores, mensagens e intervalos.  
  
1.  Use um *sinalizador* para indicar um ponto no tempo interessante em seu aplicativo.  Por exemplo, é possível usar um sinalizador para representar que o valor de uma variável atingiu um certo limite ou que uma exceção foi lançada.  
  
2.  Uma *mensagem* também marca um ponto no tempo, mas é possível usá-la para rastreamento de estilo do log.  Por exemplo, o que pode ter sido despejado em um arquivo de log agora pode ser encapsulado em uma chamada de mensagem para poder rastreá-la e visualizá-la na Visualização Simultânea. Também é possível usar a Visualização Simultânea para exportar esses dados para um arquivo CSV.  
  
3.  O *intervalo* representa um intervalo de tempo em seu aplicativo, por exemplo, uma das suas fases.  
  
## <a name="marker-linkage-to-threads"></a>Vinculação de marcador para threads  
 Cada thread que gera marcadores tem um canal separado de linha do tempo.  A ID do thread responsável por gerar os eventos de marcador é mostrada ao lado da descrição do canal do marcador.  A ID mostrada no lado esquerdo do canal do marcador corresponde à ID de outro thread no processo atual.  
  
## <a name="marker-importance"></a>Importância do marcador  
 Os marcadores podem ter um dos quatro níveis de importância: baixa, normal, alta e crítica.  É possível filtrar as fontes de marcadores com base no nível de importância.  Por exemplo, se você só desejar ver os marcadores de uma fonte específica que tem importância normal ou crítica, será possível configurar o filtro na caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md). A importância de um marcador é exibida em sua dica de ferramenta e no [Relatório de Marcadores](../profiling/markers-report.md).  
  
## <a name="marker-category"></a>Categoria de marcador  
 Uma categoria de marcador indica um grupo de eventos de marcador que vêm da mesma fonte.  A Visualização Simultânea usa cor para diferenciar diferentes categorias de sinalizadores e intervalos. É possível configurar a Visualização Simultânea para usar categorias para filtrar os eventos de marcador em um provedor de eventos específico.  Use a caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) para configurar o filtro.  
  
## <a name="known-sources-of-markers"></a>Fontes conhecidas de marcadores  
 Qualquer provedor ETW pode gerar marcadores, desde que os provedores obedeçam a determinadas restrições. É possível configurar a Visualização Simultânea para escutar outras fontes de evento para marcadores. Por padrão, ele escuta estas fontes de evento:  
  
- [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md)  
  
- [TPL (Biblioteca de Paralelismo de Tarefas)](http://msdn.microsoft.com/library/b8f99f43-9104-45fd-9bff-385a20488a23)  
  
- [Fluxo de dados](http://msdn.microsoft.com/library/643575d0-d26d-4c35-8de7-a9c403e97dd6)  
  
- [PLINQ (LINQ paralelo)](http://msdn.microsoft.com/library/3d4d0cd3-bde4-490b-99e7-f4e41be96455)  
  
- [Tempo de Execução de Simultaneidade](http://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)  
  
- [Suporte do Marcador de Cenário](http://msdn.microsoft.com/en-us/e3b55bc2-b451-4214-ae00-0c7f5a5baec8)  
  
- [C++ AMP (C++ Accelerated Massive Parallelism)](http://msdn.microsoft.com/library/e27824cb-3167-409b-8c3f-a0e476d8f349)  
  
  É possível usar a guia Marcadores na caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) para controlar se os marcadores de várias fontes são exibidos na Visualização Simultânea e é possível filtrá-los com base na importância e na categoria.  
  
## <a name="markers-from-eventsource"></a>Marcadores de EventSource  
 A Visualização Simultânea também pode exibir eventos EventSource.  Para obter mais informações, consulte [Visualizando eventos EventSource como marcadores](../profiling/visualizing-eventsource-events-as-markers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Marcadores de sinalizador](../profiling/flag-markers.md)   
 [Marcadores de mensagem](../profiling/message-markers.md)   
 [Marcadores de intervalo](../profiling/span-markers.md)   
 [Visualizando eventos EventSource como marcadores](../profiling/visualizing-eventsource-events-as-markers.md)



