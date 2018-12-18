---
title: Guia atual | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.reportnav.current
helpviewer_keywords:
- Concurrency Visualizer, Callstack at Selection Point
ms.assetid: 2c7b1ae5-3756-4795-bc59-f6bb113f2ba5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9964da1521852d942490c09b83135c62f6be3ed9
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34749493"
---
# <a name="current-tab"></a>Guia atual
Ao clicar na guia **Atual**, é possível ver uma pilha de chamadas (se disponível) que está próxima ao ponto de seleção atual na linha do tempo se um segmento de thread da CPU está selecionado.  Nesse caso, o ponto de seleção é representado por uma seta preta ou um cursor, acima da linha do tempo. Quando um segmento de bloqueio é selecionado, o cursor do sistema não é exibido porque não houve nenhuma execução. No entanto, o segmento ainda está realçado e uma pilha de chamadas é exibida.  
  
 A guia **Atual** também exibe informações sobre segmentos de atividade do DirectX, marcadores e acesso de E/S.  Para segmentos de atividade do DirectX, são exibidas informações sobre a forma como os pacotes DMA são processados pela fila de hardware.  Para os marcadores, são exibidas informações sobre a descrição e o tipo de marcador.  Para o acesso de E/S, são exibidas informações sobre o arquivo e o número de bytes lidos ou gravados.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)