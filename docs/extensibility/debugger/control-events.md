---
title: Eventos de controle | Microsoft Docs
description: Saiba mais sobre como enviar eventos durante a execução controlada do seu programa usando a interface IDebugEvent2.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 0fc63484-5fb6-4887-9ea4-1905b459ca9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb7249ece3ab38ff6f378f3c48ce36a995677604
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905690"
---
# <a name="control-events"></a>Eventos de controle
Você deve enviar eventos durante a execução controlada do seu programa. Todos os eventos são enviados usando a interface [IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md) e têm atributos que exigem que você implemente o método [IDebugEvent2:: GetAttributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md) .

## <a name="additional-methods"></a>Métodos adicionais
 Alguns eventos exigem a implementação de métodos adicionais, da seguinte maneira:

- O envio da interface [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) quando o mecanismo de depuração (de) é inicializado exige que você implemente o método [IDebugEngineCreateEvent2:: GetEngine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md) .

- O controle de execução requer a implementação de tais eventos de controle como as interfaces [IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md) e[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) . **IDebugBreakEvent2** é necessário apenas para quebras assíncronas.

- A depuração em funções requer a implementação da interface [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) e seus métodos.

  Os eventos derivados de pontos de interrupção exigem a implementação das interfaces [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md), [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)e [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) , bem como os métodos [IDebugBreakpointBoundEvent2:: GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) e [EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) .

  A avaliação de expressão assíncrona exige que você implemente a interface [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) e seus métodos [IDebugExpressionEvaluationCompleteEvent2:: GetExpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[e GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) .

  Os eventos síncronos exigem a implementação do método [IDebugEngine2:: ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) .

  Para que seu mecanismo escreva a saída em estilo de cadeia de caracteres, você deve implementar o método [IDebugOutputStringEvent2:: GetString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md) .

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
