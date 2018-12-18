---
title: Segmento da linha do tempo vazio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.empty
helpviewer_keywords:
- Concurrency Visualizer, empty timeline segment
ms.assetid: f37b301f-3edc-4e56-8084-feec2dc5a9b1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ad8d87c0574ac2c7671012fff6a81a568d6bff5f
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34764524"
---
# <a name="empty-timeline-segment"></a>Segmento vazio da linha do tempo
Na Visualização Simultânea, o motivo pelo qual uma seção da linha do tempo está vazia (tem uma tela de fundo branca) depende do tipo de canal.  
  
-   Para um canal de thread de CPU, isso significa que o thread não existia durante esta parte da linha do tempo. Se estiver interessado no thread, você poderá encontrar sua seção de execução usando o controle de aplicação de zoom ou rolando horizontalmente.  
  
-   Para um canal de E/S, significa que nenhum acesso ao disco ocorreu em nome do processo de destino no momento.  
  
-   Para um canal do DirectX, significa que nenhum trabalho de GPU foi executado em nome do processo de destino durante esta parte da linha do tempo.  
  
-   Para um canal de marcador, significa que nenhum marcador foi gerado.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Threads](../profiling/threads-view-parallel-performance.md)   
 [Controle de zoom (exibição de threads)](../profiling/zoom-control-threads-view.md)