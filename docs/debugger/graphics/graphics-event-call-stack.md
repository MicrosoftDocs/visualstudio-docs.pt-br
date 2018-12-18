---
title: Pilha de chamadas do evento de gráficos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.callstack
ms.assetid: 8a30168d-8b39-4de1-b094-c7356ba101a3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 77c53db002fd0d300a01b5cc142f6ed2daf4daa2
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510572"
---
# <a name="graphics-event-call-stack"></a>Pilha de chamadas de gráfico
A pilha de chamadas do evento de gráficos no analisador de gráficos do Visual Studio o ajuda a mapear a relação entre eventos de gráficos problemático e código-fonte do seu aplicativo.  
  
 Esta é a janela de pilha de chamadas do evento:  
  
 ![A pilha de chamadas anteriores a um evento DrawIndexed. ](media/gfx_diag_demo_graphics_event_call_stack_orientation.png "gfx_diag_demo_graphics_event_call_stack_orientation")  
  
## <a name="understanding-the-graphics-event-call-stack"></a>Noções básicas sobre a pilha de chamadas do evento de gráficos  
 Você pode usar a pilha de chamadas do evento para entender o fluxo de execução que leva a um determinado evento do Direct3D. Ele é semelhante a janela de pilha de chamadas do Visual Studio, exceto que em vez de exibir a pilha de chamadas atual do thread atual em um aplicativo em execução, ele exibe a pilha de chamadas que existia quando ocorreu o evento do Direct3D selecionado. Da pilha de chamada de evento, você pode ir para o site de chamada do evento Direct3D selecionado para inspecionar o código ao redor.  
  
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
 [Passo a passo: objetos ausentes devido ao sombreamento de vértice](walkthrough-missing-objects-due-to-vertex-shading.md)