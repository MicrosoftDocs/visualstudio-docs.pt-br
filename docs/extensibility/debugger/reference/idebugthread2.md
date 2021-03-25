---
description: Essa interface representa um thread em execução em um programa.
title: IDebugThread2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24a9cef2e62dc2597871f270c9ee48ad58c0a0e1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086970"
---
# <a name="idebugthread2"></a>IDebugThread2
Essa interface representa um thread em execução em um programa.

## <a name="syntax"></a>Sintaxe

```
IDebugThread2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar um thread de execução em um único programa.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md) para obter essa interface que representa o thread ativo no momento.

 Essa interface também é usada na criação de uma solicitação de ponto de interrupção (consulte [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)).

 Essa interface também é retornada ao resolver um ponto de interrupção associado ou de erro (consulte [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) e [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugThread2` .

|Método|Descrição|
|------------|-----------------|
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|Recupera uma lista de quadros de pilha para este thread.|
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|Obtém o nome do thread.|
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|Define o nome do thread.|
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|Obtém o programa no qual um thread está em execução.|
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|Determina se a próxima instrução pode ser definida para o quadro de pilha e o contexto de código fornecidos.|
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|Define a próxima instrução para o quadro de pilha e o contexto de código fornecidos.|
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|Obtém o identificador de thread do sistema.|
|[Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|Suspende um thread.|
|[Retomar](../../../extensibility/debugger/reference/idebugthread2-resume.md)|Retoma um thread.|
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|Obtém as propriedades que descrevem um thread.|
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|Obtém o thread lógico associado a este thread físico.|

## <a name="remarks"></a>Comentários
 Como um único thread físico pode ser executado em vários programas, mais de um `IDebugThread2` de mais de um programa pode representar o mesmo thread físico.

 Quando ocorre um ponto de interrupção ou exceção, um evento é enviado pela chamada de [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md). Um dos argumentos para esse método é uma `IDebugThread2` interface que representa o thread atual. [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) é usado para obter a interface [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) para o quadro de pilhas atual.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
