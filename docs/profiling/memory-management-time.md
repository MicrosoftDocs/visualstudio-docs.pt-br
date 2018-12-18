---
title: Tempo de gerenciamento da memória | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0284d312a4157c41f93fec17d601406c669a83c1
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35238245"
---
# <a name="memory-management-time"></a>Tempo de gerenciamento de memória
Esses segmentos na linha do tempo estão associados os tempos de bloqueio categorizados como Gerenciamento da Memória. Esse cenário significa que um thread está bloqueado por um evento associado a uma operação de gerenciamento de memória, como paginação. Durante esse tempo, um thread foi bloqueado em um estado de API ou kernel que a Visualização Simultânea está contando como gerenciamento de memória. Eles incluem eventos como paginação e alocação de memória.  
  
 Examine os relatórios de perfil e as pilhas de chamada associados para entender melhor os motivos subjacentes para os bloqueios categorizados como Gerenciamento de Memória.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)