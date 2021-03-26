---
title: Tipos de evento com suporte | Microsoft Docs
description: Saiba mais sobre os tipos de eventos aos quais a depuração do Visual Studio dá suporte, incluindo eventos assíncronos, eventos síncronos e eventos de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 883c9fd51cc4dfc4f2cc2f996d24c0722478505f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079404"
---
# <a name="supported-event-types"></a>Tipos de eventos com suporte
A depuração do Visual Studio atualmente dá suporte aos seguintes tipos de evento:

- Eventos assíncronos

   Notifique o SDM (Gerenciador de depuração de sessão) e o IDE que o estado do aplicativo que está sendo depurado está sendo alterado. Esses eventos são processados ao lazer do SDM e do IDE. Nenhuma resposta é enviada para o mecanismo de depuração (DE) depois que o evento é processado. As interfaces [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md) e [IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md) são exemplos de eventos assíncronos.

- Eventos síncronos

   Notifique o SDM e o IDE que o estado do aplicativo que está sendo depurado está sendo alterado. A única diferença entre esses eventos e eventos assíncronos é que uma resposta é enviada por meio do método [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) .

   O envio de um evento síncrono é útil se você precisar que seu DE continue o processamento depois que o IDE receber e processar o evento.

- Eventos de interrupção síncronos ou interrupção de eventos

   Notifique o SDM e o IDE que o aplicativo que está sendo depurado parou de executar o código. Quando você envia um evento de parada por meio do [evento](../../extensibility/debugger/reference/idebugeventcallback2-event.md)Method, o parâmetro [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) é obrigatório. A interrupção de eventos é continuada por uma chamada para um dos seguintes métodos:

  - [Executar](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [Continuar](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    As interfaces [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) e [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) são exemplos de como parar eventos.

  > [!NOTE]
  > Eventos de interrupção assíncrona não são suportados. É um erro enviar um evento de parada assíncrona.

## <a name="discussion"></a>Discussão
 A implementação real de eventos depende do design de DE. O tipo de cada evento enviado é determinado por seus atributos, que são definidos quando você cria o DE. Por exemplo, um DE pode enviar um [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) como um evento assíncrono, enquanto outro pode enviá-lo como um evento de interrupção.

 A tabela a seguir especifica quais parâmetros de programa e thread são necessários para quais eventos, bem como tipos de evento. Qualquer evento pode ser síncrono. Nenhum evento precisa ser síncrono.

> [!NOTE]
> A interface [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) é necessária para todos os eventos.

|Evento|IDebugProgram2|IDebugThread2|Interrompendo eventos|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|Obrigatório|Obrigatório|No|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|Não permitido|Não permitido|Não|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|Não permitido|Não permitido|Não|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Pode ser|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Pode ser|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Pode ser|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|Obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|Obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|Obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|Obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|Obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|IDebugStopCompleteEvent2|Obrigatório|Obrigatório|Yes|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|Obrigatório|Obrigatório|Yes|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|Obrigatório|Obrigatório|No|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|Obrigatório|Obrigatório|No|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|Permitido, mas não obrigatório|Permitido, mas não obrigatório|Não|

## <a name="see-also"></a>Confira também
- [Enviando eventos](../../extensibility/debugger/sending-events.md)
