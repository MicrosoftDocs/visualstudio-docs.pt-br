---
title: Exibição Resumo – Exibição de contenção de recursos | Microsoft Docs
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
- Summary view
ms.assetid: 6da57b83-7b42-4d7c-9aea-8e0a830faf6b
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 45052997e9dd8332518ce5fb7804963f88e97959
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791846"
---
# <a name="summary-view---resource-contention-view"></a>Exibição Resumo – Exibição de contenção de recursos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição Resumo exibe informações sobre os eventos no aplicativo nos quais um thread ou processo foi suspenso enquanto aguardava o acesso a um recurso.  
  
 Para obter mais informações, incluindo uma descrição das listas Links de notificação e Relatório, consulte [Exibição Resumo](../profiling/summary-view.md).  
  
## <a name="timeline-graph"></a>Gráfico de linha do tempo  
 O gráfico de linha do tempo na exibição Resumo mostra o número de eventos de contenção do aplicativo com perfil ao longo do tempo em que ocorreu a criação de perfil. É possível usar o gráfico de linha do tempo para filtrar a exibição para um intervalo de tempo selecionado. Para obter mais informações, consulte [Como filtrar exibições de relatório por meio da linha do tempo de resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md).  
  
## <a name="most-contended-resources"></a>Recursos com Mais Contenção  
 **Recursos com mais contenções** lista os recursos no aplicativo que causaram a maioria dos eventos de contenção. É possível clicar em um nome de recurso para mostrar a exibição Contenções. A exibição Contenções fornece uma linha do tempo detalhada das contenções de recursos por thread.  
  
 **Recursos com mais contenções** inclui os dados a seguir para cada recurso.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do recurso.|  
|**% de contenções**|O percentual de todos os eventos de contenção nos dados de criação de perfil que foram contenções sobre esse recurso.|  
  
## <a name="most-contended-thread"></a>Thread com mais contenção  
 **Threads com mais contenções** lista os threads no aplicativo que tiveram o maior número de eventos de contenção. É possível clicar em um nome de thread para mostrar a exibição Contenções que fornece uma linha do tempo detalhada das contenções de recursos pelo thread.  
  
 **Threads com mais contenções** inclui os dados a seguir para cada thread.  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID**|O identificador de thread.|  
|**Nome**|O nome do processo que é o proprietário do thread.|  
|**% de contenções**|O percentual de todos os eventos de contenção nos dados de criação de perfil que foram contenções sobre esse recurso.|



