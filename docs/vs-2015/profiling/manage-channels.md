---
title: Gerenciar Canais | Microsoft Docs
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
- vs.cv.threads.tools.managechannels
helpviewer_keywords:
- Concurrency Visualizer, Manage Channels
ms.assetid: 507b06e9-bb56-4a72-8fd5-f91f958da6fc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dba4def686f97bd3169eb5816630c272dc61d8e6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726000"
---
# <a name="manage-channels"></a>Gerenciar canais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em **Exibição de Threads** na Visualização Simultânea, você pode organizar os canais para o seu processo, de forma que você possa examinar padrões específicos. Você pode classificar os canais, movê-los para cima e para baixo, ocultá-los ou mostrá-los.  
  
## <a name="sort-by"></a>Classificar por  
 Você pode usar o controle Classificar por para classificar os threads por critérios diferentes, com base no nível de zoom atual. Isso é especialmente útil quando você estiver procurando por um determinado padrão. Você pode classificar por estes critérios:  
  
|Critério|Definição|  
|--------------|----------------|  
|Hora de início|Classifica os threads de acordo com os horários de início. Essa é a ordem de classificação padrão.|  
|Hora de término|Classifica os threads de acordo com os horários de término.|  
|Execução|Classifica os threads de acordo com o percentual de tempo gasto na execução.|  
|Sincronização|Classifica os threads de acordo com o percentual de tempo gasto na sincronização.|  
|E/S|Classifica os threads de acordo com o percentual de tempo gasto na entrada/saída (leitura e gravação de dados).|  
|Sleep|Classifica os threads de acordo com o percentual de tempo gasto no modo de suspensão.|  
|Paginação|Classifica os threads de acordo com o percentual de tempo gasto na paginação.|  
|Preempção|Classifica os threads de acordo com o percentual de tempo gasto na preempção.|  
|Processamento de interface do usuário|Classifica os threads de acordo com o percentual de tempo gasto no processamento da interface do usuário.|  
  
## <a name="move-selected-channel-up-or-down"></a>Mover o canal selecionado para cima ou para baixo  
 Você pode usar esses controles para mover um canal para cima ou para baixo na lista. Por exemplo, você pode posicionar os canais relacionados próximos uns dos outros para ajudar você a examinar um padrão específico ou uma relação entre threads.  
  
## <a name="move-selected-channel-to-top-or-bottom"></a>Mover o canal selecionado para a parte superior ou inferior  
 Você pode mover os canais selecionados para a parte superior ou inferior da lista para que você pode examinar um determinado padrão ou mover alguns canais para fora do caminho enquanto examina outros.  
  
## <a name="hide-selected-channels"></a>Ocultar Canais Selecionados  
 Escolha este controle quando quiser ocultar canais. Por exemplo, se um thread tiver 100 por cento da sincronização da vida útil de seu processo gerenciado, você poderá ocultá-lo ao analisar outros threads.  
  
> [!NOTE]
>  Ocultar um thread também o remove do horário de cálculo, que é mostrado na legenda ativa e nos relatórios do perfil.  
  
## <a name="show-all-channels"></a>Mostrar todos os canais  
 Esse controle é ativado quando um ou mais canais estão ocultos. Se você clicar nele, todos os elementos ocultos serão mostrados e retornados aos cálculos de tempo.  
  
## <a name="move-markers-to-top"></a>Mova os marcadores para o início  
 Se um rastreamento tiver eventos de marcador, você poderá usar esse comando para mover os canais de marcador para o início da linha do tempo. Sua ordem relativa é preservada.  
  
## <a name="group-markers-by-thread"></a>Agrupar Marcadores por Thread  
 Se um rastreamento tiver eventos de marcador, você poderá usar esse comando para os canais do marcador de grupo sob o thread que gerou os eventos do marcador.  Os canais de disco são movidos para a parte superior da lista de canais e os canais GPU são movidos para a parte inferior.  
  
## <a name="see-also"></a>Consulte também  
 [Controle de Zoom (Exibição de Threads)](../profiling/zoom-control-threads-view.md)   
 [Ativar/desativar modo de medidas](../profiling/measure-mode-on-off.md)   
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)



