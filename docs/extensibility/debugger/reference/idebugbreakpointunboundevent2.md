---
description: Essa interface diz ao SDM (Gerenciador de depuração de sessão) que um ponto de interrupção associado foi desassociado de um programa carregado.
title: IDebugBreakpointUnboundEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2
ms.assetid: 6b1e1863-0c64-4d85-8ab9-aface522fdea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27c032c1563bf208c378044b4e093529a2dba10c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088634"
---
# <a name="idebugbreakpointunboundevent2"></a>IDebugBreakpointUnboundEvent2
Essa interface diz ao SDM (Gerenciador de depuração de sessão) que um ponto de interrupção associado foi desassociado de um programa carregado.

## <a name="syntax"></a>Sintaxe

```
IDebugBreakpointUnboundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para pontos de interrupção. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface (o SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface).

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia esse objeto DE evento quando um ponto de interrupção associado é desassociado. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugBreakpointUnboundEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)|Obtém o ponto de interrupção que se tornou desassociado.|
|[GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)|Obtém o motivo pelo qual o ponto de interrupção foi desassociado.|

## <a name="remarks"></a>Comentários
 Quando uma DLL ou uma classe do mecanismo de depuração é descarregada, todos os pontos de interrupção que foram associados ao código nesse módulo devem ser desassociados do programa que está sendo depurado. Um `IDebugBreakpointUnboundEvent2` é enviado para cada ponto de interrupção não associado.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
