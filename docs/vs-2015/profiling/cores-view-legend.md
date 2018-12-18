---
title: Legenda da exibição de núcleos | Microsoft Docs
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
- vs.cv.cores.legend
helpviewer_keywords:
- Concurrency Visualizer, Cores View Legend
ms.assetid: e160384c-fcfe-49b3-86b7-229adb736c51
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2c00b6ccf56eb9e171fbaf9afdaea1828b5a1325
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783097"
---
# <a name="cores-view-legend"></a>Legenda da exibição de núcleos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A legenda da Exibição de Núcleos identifica cada thread pela cor e pelo nome. Ela inclui colunas que mostram contagens de alternâncias de contexto de núcleo cruzado, o total de alternâncias de contexto e o percentual de alternâncias de contexto que cruzam núcleos. As linhas na legenda são classificadas pelo número de alternâncias de contexto de núcleo cruzado, em ordem decrescente.  
  
 É possível selecionar linhas na legenda para filtrar os threads exibidos na linha do tempo. Apenas os threads selecionados são mostrados na linha do tempo. Se nenhuma linha estiver selecionada, todas as linhas serão mostradas na linha do tempo.  
  
 Alternâncias de contexto de núcleo cruzado são mais caras em sobrecarga e desempenho do que alternâncias que permanecem no mesmo núcleo lógico. Durante alternâncias de contexto, os registros do processador são salvos e restaurados, o código de kernel do sistema operacional é executado, as entradas de buffer à parte de translação são recarregadas e o pipeline do processador é liberado. Alternâncias de contexto de núcleo cruzado podem ser ainda mais caras do que outras alternâncias de contexto, pois os dados do cache não são válidos para esse thread em outro núcleo. Por outro lado, se um thread tiver alternância de contexto para o núcleo em que foi executado anteriormente, é provável que os dados úteis ainda estejam no cache. Quando as alternâncias de contexto de núcleo cruzado aumentarem devido a tentativas de gerenciar a afinidade de thread e o desempenho for prejudicado, considere a possibilidade de resolver esse problema. Comece eliminando a afinidade de thread e, em seguida, observe o comportamento de núcleo cruzado resultante.  
  
 A tabela a seguir descreve os elementos da legenda.  
  
|Elemento|Definição|  
|-------------|----------------|  
|Nome do Thread|Mostra a cor do thread na linha do tempo dos núcleos anteriores e o nome do thread.|  
|Opções de contexto de núcleo cruzado|O número de alternâncias de contexto para um thread que também mudou de um núcleo lógico para outro. Ele não diferencia entre alternâncias de contexto de núcleo cruzado que cruzam de uma matriz do processador para outra e aqueles que permanecem na mesma matriz.|  
|Opções de Contexto Total|O número total de alternâncias de contexto de determinado thread durante o período de amostragem. Sempre que um thread muda de contexto (por exemplo, de execução para sincronização), uma alternância de contexto é contada.|  
|Porcentagem de alternâncias de contexto que cruzam núcleos|Calculado como um percentual, dividindo o número de alternâncias de contexto de núcleo cruzado pelo número do total de alternâncias de contexto. Quanto maior esse percentual, maior será o efeito geral da sobrecarga de alternâncias de contexto de núcleo cruzado sobre o desempenho desse thread específico.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de núcleos](../profiling/cores-view.md)



