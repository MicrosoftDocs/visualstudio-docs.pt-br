---
title: Tempo de gerenciamento da memória | Microsoft Docs
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
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b3fc38abb47c70949b63b44958e96e3b168589fd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51729425"
---
# <a name="memory-management-time"></a>Hora de gerenciamento da memória
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esses segmentos na linha do tempo estão associados os tempos de bloqueio categorizados como Gerenciamento da Memória. Isso significa que um thread é bloqueado por um evento associado uma operação de gerenciamento de memória, como paginação. Durante esse tempo, um thread foi bloqueado em um estado de API ou kernel que a Visualização Simultânea está contando como gerenciamento de memória. Eles incluem eventos como paginação e alocação de memória.  
  
 Examine os relatórios de perfil e as pilhas de chamada associados para entender melhor os motivos subjacentes para os bloqueios categorizados como Gerenciamento de Memória.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)



