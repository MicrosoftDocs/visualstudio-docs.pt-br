---
title: Canais (exibição de threads) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.channelnames
helpviewer_keywords:
- Concurrency Visualizer, Channels (Threads View)
ms.assetid: 2f798c17-2363-42a4-be94-a5751d208eac
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f18a636d83210b2329d103b1babdf47e697fd5c7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537079"
---
# <a name="channels-threads-view"></a>Canais (exibição de threads)
A Visualização Simultânea mostra quatro tipos de canais: canais de thread, canais de disco, canais de marcador e canais da GPU.

## <a name="thread-channels"></a>Canais de thread
 Um canal de thread mostra o estado do thread, por cor, para apenas um thread. Quando você pausa no nome do canal, a função de início para o thread determinado é exibida. A Visualização Simultânea detecta vários tipos de threads. Os tipos mais comuns são mostrados na tabela a seguir.

|Thread|Descrição|
|-|-|
|Thread principal|O thread que iniciou o aplicativo.|
|Thread de trabalho|Um thread que foi criado pelo thread principal do aplicativo.|
|Thread de trabalho CLR|Um thread de trabalho que foi criado pelo CLR (Common Language Runtime).|
|Depurador Auxiliar|Um thread de trabalho que foi criado pelo depurador do Visual Studio.|
|Thread ConcRT|Um thread que foi criado pelo Runtime de Simultaneidade Microsoft.|
|Thread GDI|Um thread que foi criado por GDIPlus.|
|Thread OLE/RPC|Um thread que foi criado como um Thread de Trabalho do RPC.|
|Thread RPC|Um thread que foi criado como um Thread do RPC.|
|Thread de Winsock|Um thread que foi criado como um Thread do Winsock.|
|Pool de Threads|Um thread que foi criado pelo Pool de Threads do CLR.|

## <a name="disk-channels"></a>Canais de disco
 Canais de disco correspondem a unidades físicas no computador. Uma vez que existem canais separados para operações de Leitura e Gravação para cada unidade física no sistema, cada unidade tem dois canais. Os números de disco correspondem aos nomes de dispositivo de kernel. Um canal de disco será mostrado somente se tiver ocorrido atividade no disco.

## <a name="marker-channels"></a>Canais do marcador
 Canais do marcador correspondem aos eventos gerados pelo aplicativo e às bibliotecas que ele usa. Por exemplo, a Biblioteca de Paralelismo de Tarefas, a Biblioteca de Padrões Paralelos e o AMP C++ geram eventos exibidos como marcadores. Cada canal de marcador é associado uma ID de thread, que é exibido ao lado da descrição do canal. A ID identifica o thread que gerou o evento. A descrição do canal inclui o nome do provedor ETW (Rastreamento de Eventos para Windows ) que gerou os eventos. Se o canal exibir eventos do [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md), o nome da série também será exibido.

## <a name="gpu-channels"></a>Canais de GPU
 Canais da GPU exibem informações sobre a atividade do DirectX 11 no sistema.  Cada mecanismo DirectX associado à placa gráfica tem um canal separado.  Os segmentos individuais representam o tempo gasto no processamento de um pacote DMA.

## <a name="see-also"></a>Confira também
- [Exibição de threads](../profiling/threads-view-parallel-performance.md)