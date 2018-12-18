---
title: Suporte para tipos de evento | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: dd6f8f5b7c2782bb908538426cb531db216b72fb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781459"
---
# <a name="supported-event-types"></a>Tipos de eventos com suporte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Depuração do Visual Studio atualmente dá suporte aos seguintes tipos de evento:  
  
- Eventos assíncronos  
  
   Notificar o Gerenciador de sessão de depuração (SDM) e o IDE que o estado do aplicativo que está sendo depurado está mudando. Esses eventos são processados em tempo de livre do SDM e o IDE. Nenhuma resposta é enviada para o mecanismo de depuração (DES) depois que o evento seja processado. O [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md) e [IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md) interfaces são exemplos de eventos assíncronos.  
  
- Eventos síncronos  
  
   Notificar o SDM e o IDE que está alterando o estado do aplicativo que está sendo depurado. A única diferença entre esses eventos e eventos assíncronos é que uma resposta é enviada por meio das [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) método.  
  
   Enviar um evento síncrono é útil se você precisar DE sua para continuar o processamento depois que o IDE recebe e processa o evento.  
  
- Eventos de parada de síncrona ou eventos de parada  
  
   Notificar o SDM e o IDE que o aplicativo que está sendo depurado parou de executar o código. Quando você envia um evento de interrupção por meio do método [evento](../../extensibility/debugger/reference/idebugeventcallback2-event.md), o [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) o parâmetro é obrigatório. Interrompendo eventos foram mantidos por uma chamada para um dos seguintes métodos:  
  
  - [Executar](../../extensibility/debugger/reference/idebugprogram2-execute.md)  
  
  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)  
  
  - [Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)  
  
    As interfaces [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) e [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) são exemplos de eventos de interrupção.  
  
  > [!NOTE]
  >  Não há suporte para eventos de interrupção assíncrona. É um erro ao enviar um evento de interrupção assíncrono.  
  
## <a name="discussion"></a>Discussão  
 A implementação real de eventos depende do design do seu DE. O tipo de cada evento enviado é determinado por seus atributos, que são definidos quando você projeta a Alemanha. Por exemplo, um Alemanha pode enviar uma [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) como um evento assíncrono, enquanto outro pode enviá-lo como um evento de interrupção.  
  
 A tabela a seguir especifica quais parâmetros de thread e programa são necessários para o qual eventos, bem como os tipos de evento. Qualquer evento pode ser síncrono. Nenhum evento precisa ser síncronas.  
  
> [!NOTE]
>  O [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) interface é necessária para todos os eventos.  
  
|evento|IDebugProgram2|IDebugThread2|Eventos de parada|  
|-----------|--------------------|-------------------|---------------------|  
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|Necessária|Necessária|Sim|  
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|Necessária|Necessária|Sim|  
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|Necessária|Necessária|Não|  
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|Não permitido|Não permitido|Não|  
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|Não permitido|Não permitido|Não|  
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|Necessária|Necessária|Sim|  
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Pode ser|  
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|Necessária|Necessária|Sim|  
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Pode ser|  
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|Necessária|Necessária|Sim|  
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|Necessária|Necessária|Sim|  
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Pode ser|  
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|Necessária|Permitido, mas não obrigatórios|Não|  
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|Necessária|Permitido, mas não obrigatórios|Não|  
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|Necessária|Permitido, mas não obrigatórios|Não|  
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|Necessária|Permitido, mas não obrigatórios|Não|  
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|Necessária|Permitido, mas não obrigatórios|Não|  
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|IDebugStopCompleteEvent2|Necessária|Necessária|Sim|  
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|Necessária|Necessária|Sim|  
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|Necessária|Necessária|Não|  
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|Necessária|Necessária|Não|  
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|Permitido, mas não obrigatórios|Permitido, mas não obrigatórios|Não|  
  
## <a name="see-also"></a>Consulte também  
 [Enviar eventos](../../extensibility/debugger/sending-events.md)

