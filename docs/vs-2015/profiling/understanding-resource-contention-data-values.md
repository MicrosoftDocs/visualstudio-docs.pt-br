---
title: Noções Básicas sobre valores de dados de contenção de recurso | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
ms.assetid: 071c0f0f-1eba-4dc8-ae87-0810e4086dd0
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 64bad925b7d0ac6170a4ac581fc327450aa2dd04
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948108"
---
# <a name="understanding-resource-contention-data-values"></a>Noções básicas sobre valores de dados de contenção de recurso
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Perfis de contenção de recursos coletam informações de pilha de chamadas detalhadas sempre que segmentos concorrentes em um aplicativo são forçados a aguardar o acesso a um recurso compartilhado.  
  
 **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  Relatórios de contenção do recurso exibem o número total de contenções e o tempo total gasto aguardando um recurso para os módulos, funções, linhas de código-fonte e instruções no qual ocorreu a espera.  
  
- Valores inclusivos exibem o número total de contenções que forçou uma função a espera por contenção de recursos e o tempo total que a função esperou.  Contenções que foram causadas por funções filho que foram chamadas pela função são incluídas nos valores inclusivos.  
  
- Valores exclusivos exibem apenas o número de contenções que forçaram uma função a esperar e que foram causadas pelo código no corpo da função. Contenções causadas por funções filho não são incluídas. O tempo exclusivo para a função também inclui somente os tempos de espera que foram causados por instruções no corpo da função.  
  
  Exibições de relatório de contenção de recursos também incluem gráficos de linha do tempo que mostram os eventos de contenção individuais ao longo do tempo e mostram as pilhas de chamadas que criaram o evento específico. Para obter mais informações, consulte um dos seguintes tópicos:  
  
- [Exibição de detalhes do thread](../profiling/thread-details-view-contention-data.md)  
  
- [Exibição de detalhes do recurso](../profiling/resource-details-view-contention-data.md)  
  
  Para obter mais informações sobre o segundo modo de criação de perfil de simultaneidade, consulte [Visualização Simultânea](../profiling/concurrency-visualizer.md).



