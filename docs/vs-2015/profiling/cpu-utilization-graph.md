---
title: Gráfico de utilização da CPU | Microsoft Docs
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
- vs.cv.cpu.graph
helpviewer_keywords:
- CPU Utilization GraphConcurrency Visualizer, CPU Utilization Graph
ms.assetid: 5332fd38-622d-47a3-874f-8c2fd7a30f95
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b1eb8baeee066336834cc1fcfe427512108387a3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727006"
---
# <a name="cpu-utilization-graph"></a>Gráfico de utilização da CPU
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O gráfico de Utilização da CPU mostra o nível de utilização em um aplicativo ao longo do tempo. O eixo X representa a duração do rastreamento e o eixo Y representa o número de núcleos lógicos no sistema. O gráfico não mostra qual núcleo específico está ativo em determinado momento. Por exemplo, se dois núcleos estiverem sendo executados individualmente com capacidade de 50% durante um período específico, essa exibição mostrará um núcleo lógico sendo utilizado.  
  
## <a name="cpu-utilization-graph-colors"></a>Cores do gráfico de Utilização da CPU  
  
-   Verde indica a utilização dos núcleos lógicos no sistema pelo processo atual.  
  
-   Cinza-claro indica a utilização de núcleos lógicos por outros processos no sistema. Um alto percentual de cinza-claro no gráfico da CPU indica que o sistema está muito carregado por outros processos e que o processo provavelmente será impedido por eles. Para reduzir o consumo de núcleos lógicos por outros processos, reduza o número deles em execução no sistema.  
  
-   Cinza-escuro indica o consumo de núcleos lógicos pelo processo do sistema. Não é possível controlar isso diretamente, mas é útil saber quando isso está ocorrendo, pois pode afetar a disponibilidade de núcleos lógicos para o processo.  
  
-   Branco indica a disponibilidade de núcleos lógicos não utilizados no sistema. Esses núcleos estarão disponíveis para o processo se você puder encontrar mais oportunidades de paralelismo.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Utilização](../profiling/utilization-view.md)   
 [Utilização da CPU média](../profiling/average-cpu-utilization.md)



