---
title: Pilha de chamadas do evento de gráficos | Microsoft Docs
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
- vs.graphics.callstack
ms.assetid: 8a30168d-8b39-4de1-b094-c7356ba101a3
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7c6ac7860fe846c86d846fd668c4647cd4145756
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762845"
---
# <a name="graphics-event-call-stack"></a>Pilha de chamadas de gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A pilha de chamadas do evento de gráficos no analisador de gráficos do Visual Studio o ajuda a mapear a relação entre eventos de gráficos problemático e código-fonte do seu aplicativo.  
  
 Esta é a janela de pilha de chamadas do evento:  
  
 ![A pilha de chamadas anteriores um evento DrawIndexed. ](../debugger/media/gfx-diag-demo-graphics-event-call-stack-orientation.png "gfx_diag_demo_graphics_event_call_stack_orientation")  
  
## <a name="understanding-the-graphics-event-call-stack"></a>Noções básicas sobre a pilha de chamadas do evento de gráficos  
 Você pode usar a pilha de chamadas do evento para entender o fluxo de execução que leva a um determinado evento do Direct3D. Ele é semelhante a janela de pilha de chamadas do Visual Studio, exceto que em vez de exibir a pilha de chamadas atual do thread ativo em um aplicativo em execução, ele exibe a pilha de chamadas que existia quando ocorreu o evento do Direct3D selecionado. Da pilha de chamada de evento, você pode ir para o site de chamada do evento Direct3D selecionado para inspecionar o código ao redor.  
  
 Ao usar a pilha de chamadas do evento para identificar o caminho de código do qual se origina um evento de problema, você pode usar seu conhecimento da Base de código para deduzir possíveis origens do problema, ou você pode adicionar pontos de interrupção no código-fonte do seu aplicativo para que você possa usar tradicional técnicas para examinar como o estado dos parâmetros de evento ou de aplicativo estão causando o evento a ser inadequados de depuração. Esse exame pode ajudá-lo a encontrar problemas no código-fonte que são manifestados somente como problemas de renderização.  
  
### <a name="graphics-event-call-stack-information"></a>Informações sobre a pilha de chamadas de gráfico  
 A pilha de chamadas do evento não dá suporte a eventos de pré-quadros ou definidos pelo usuário. A pilha de chamadas de eventos de gráficos é exibida em um formato de tabela.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Nome**|Um símbolo que identifica a função que contém o site de chamada. O símbolo de depuração da função é exibido quando ela está disponível. Caso contrário, o deslocamento de função é exibido.|  
|**Arquivo**|O nome do arquivo do código-fonte ou arquivo de biblioteca que contém o site de chamada.|  
|**Local**|O número de linha do site de chamada.|  
  
### <a name="links-to-graphics-objects"></a>Links a objetos de gráficos  
 Para entender o evento de gráficos selecionado, você pode precisar obter informações sobre os objetos Direct3D que estão associados ele. O **pilha de chamadas do evento de gráficos** janela fornece links para essas informações.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: objetos ausentes devido ao sombreamento de vértice](../debugger/walkthrough-missing-objects-due-to-vertex-shading.md)



