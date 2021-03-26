---
description: Essa interface diz ao SDM (Gerenciador de depuração de sessão) que um ponto de interrupção pendente foi associado com êxito a um programa carregado.
title: IDebugBreakpointBoundEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2
helpviewer_keywords:
- IDebugBreakpointBoundEvent2
ms.assetid: 24ba362e-5be1-481a-b071-e1ebd3cae6e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 80f4214139b1698ebc5de25fef923615b407063a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088712"
---
# <a name="idebugbreakpointboundevent2"></a>IDebugBreakpointBoundEvent2
Essa interface diz ao SDM (Gerenciador de depuração de sessão) que um ponto de interrupção pendente foi associado com êxito a um programa carregado.

## <a name="syntax"></a>Sintaxe

```
IDebugBreakpointBoundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface como parte de seu suporte para pontos de interrupção. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface (o SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface).

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia esse objeto DE evento quando um ponto de interrupção pendente é associado com êxito ao programa que está sendo depurado. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugBreakpointBoundEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que está sendo associado.|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)|Cria um enumerador de pontos de interrupção que foram associados a este evento.|

## <a name="remarks"></a>Comentários
 Sempre que um ponto de interrupção é associado, um evento é enviado para o SDM. Se o ponto de interrupção não puder ser associado, um [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) será enviado; caso contrário, um `IDebugBreakpointBoundEvent2` será enviado.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
