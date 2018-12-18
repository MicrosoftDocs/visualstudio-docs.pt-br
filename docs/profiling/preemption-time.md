---
title: Tempo de preempção | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.preemption
helpviewer_keywords:
- Concurrency Visualizer, Preemption Time
ms.assetid: 6b78f91e-a006-440c-83fb-e7368040951d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0d0959f5e2725401424d0231ccd286b7835a7315
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894385"
---
# <a name="preemption-time"></a>Tempo de preempção
Esses segmentos na linha do tempo estão associados aos tempos de bloqueio categorizados como Preempção. Esta categoria implica que um thread é alternado devido a um destes motivos:  
  
- O agendador substituiu usando um thread de prioridade mais alta.  
  
- O quantum de execução do thread expirou e outros threads estavam prontos para execução.  
  
  Durante esse tempo, um thread foi bloqueado pelo motivo de espera do kernel, que a Visualização Simultânea está contando como preempção. Os segmentos de preempção são iniciados quando um thread é enviado de um núcleo lógico e terminam quando esse thread continua a execução.  
  
  A dica de ferramenta para um segmento de preempção exibe o nome do processo ou do thread que causou a preempção. No entanto, isso não significa que o processo ou thread que assumiu o controle foi realmente executado durante o período de admitiu preempção.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)