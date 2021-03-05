---
description: Essa interface representa um ponto de interrupção associado a um local de código.
title: IDebugBoundBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2
helpviewer_keywords:
- IDebugBoundBreakpoint2 interface
ms.assetid: df33c52e-ded2-48a0-951d-1f36c8fc922e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2726a2422c49335d9c95e7d500381ad1fdc0108
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167471"
---
# <a name="idebugboundbreakpoint2"></a>IDebugBoundBreakpoint2
Essa interface representa um ponto de interrupção associado a um local de código.

## <a name="syntax"></a>Sintaxe

```
IDebugBoundBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para pontos de interrupção.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [BIND](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) cria essa interface. As chamadas para [getbreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md) e [Next](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md) também podem obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugBoundBreakpoint2` .

|Método|Descrição|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente do qual o ponto de interrupção associado especificado foi criado.|
|[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|Obtém o estado deste ponto de interrupção associado.|
|[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)|Obtém a contagem de sucessos atual para este ponto de interrupção associado.|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|Obtém a resolução do ponto de interrupção que descreve esse ponto de interrupção.|
|[Habilitar](../../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|Habilita ou desabilita o ponto de interrupção.|
|[SetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-sethitcount.md)|Define a contagem de acesso para este ponto de interrupção associado.|
|[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)|Define ou altera a condição associada a este ponto de interrupção associado.|
|[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)|Define ou altera a contagem de aprovações associada a este ponto de interrupção associado.|
|[Delete (excluir)](../../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|Exclui o ponto de interrupção.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)
- [Associa](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
