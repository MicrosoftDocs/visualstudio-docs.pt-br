---
description: Essa interface representa um ponto de interrupção que está pronto para ser associado a um local de código.
title: IDebugPendingBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a52856cfa70491b7a7daa9079c111b1430475d22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053705"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
Essa interface representa um ponto de interrupção que está pronto para ser associado a um local de código.

## <a name="syntax"></a>Sintaxe

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para pontos de interrupção.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) cria um ponto de interrupção pendente de uma interface [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) . Uma chamada para [BIND](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) cria uma `IDebugBreakpoint2` interface que representa um ponto de interrupção associado no programa.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugPendingBreakpoint2` .

|Método|Descrição|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|Determina se esse ponto de interrupção pendente pode ser associado a um local de código.|
|[Associa](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|Associa esse ponto de interrupção pendente a um ou mais locais de código.|
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|Obtém o estado deste ponto de interrupção pendente.|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|Obtém a solicitação de ponto de interrupção que foi usada para criar esse ponto de interrupção pendente.|
|[Virtualizar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|Alterna o estado virtualizado deste ponto de interrupção pendente.|
|[Habilitar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|Alterna o estado habilitado deste ponto de interrupção pendente.|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|Define ou altera a condição associada a esse ponto de interrupção pendente.|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|Define ou altera a contagem de aprovações associada a esse ponto de interrupção pendente.|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|Enumera todos os pontos de interrupção associados a este ponto de interrupção pendente.|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|Enumera todos os pontos de interrupção de erro que resultaram desse ponto de interrupção pendente.|
|[Excluir](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|Exclui esse ponto de interrupção pendente e todos os pontos de interrupção associados a ele.|

## <a name="remarks"></a>Comentários
 `IDebugPendingBreakpoint2` pode ser pensado como um provedor de todas as informações necessárias para associar um ponto de interrupção ao código que pode ser aplicado a um ou vários programas.

 Um ponto de interrupção pendente pode potencialmente produzir mais de um ponto de interrupção associado. Por exemplo, um ponto de interrupção em um modelo estilo C++ poderia produzir um ponto de interrupção associado para cada instância exclusiva desse modelo.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
