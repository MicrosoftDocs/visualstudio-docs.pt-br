---
title: Tempo de Suspensão | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.sleep
helpviewer_keywords:
- Concurrency Visualizer, Sleep Time
ms.assetid: 3ddb96f9-9bda-4a68-ad4d-ef488a0a68dc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b94b1695eb36aa8f55847c21a14d72357d51a405
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668158"
---
# <a name="sleep-time"></a>Tempo de suspensão
Esses segmentos na linha do tempo estão associados os tempos de bloqueio categorizados como Suspensão. A categoria de suspensão indica que um thread voluntariamente cedeu seu núcleo lógico e não está trabalhando. Durante esse tempo, um thread foi bloqueado em uma API que a Visualização Simultânea está contando como suspensão. APIs como `Sleep()` e `SwitchToThread()` pertencem a esse grupo.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de threads](../profiling/threads-view-parallel-performance.md)