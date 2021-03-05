---
description: O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) quando uma exceção é lançada no programa que está sendo executado no momento.
title: IDebugExceptionEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e171154d933ac533f6a63469321b5a0d22e8651b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152761"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) quando uma exceção é lançada no programa que está sendo executado no momento.

## <a name="syntax"></a>Sintaxe

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para relatar que ocorreu uma exceção no programa que está sendo depurado. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para relatar uma exceção. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugExceptionEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|Obtém informações detalhadas sobre a exceção que disparou este evento.|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|Obtém uma descrição legível para a exceção gerada que disparou este evento.|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|Determina se o mecanismo de depuração (DE) dá suporte à opção de passar essa exceção para o programa que está sendo depurado quando a execução é retomada.|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|Especifica se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada ou se a exceção deve ser descartada.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Comentários
 Antes de enviar o evento, o DE verifica para ver se esse evento DE exceção foi designado como uma exceção de primeira chance ou de segunda chance por uma chamada anterior para [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md). Se tiver sido designado para ser uma exceção de primeira chance, o `IDebugExceptionEvent2` evento será enviado para o SDM. Caso contrário, o DE dá ao aplicativo uma chance de lidar com a exceção. Se nenhum manipulador de exceção for fornecido, e se a exceção tiver sido designada como uma exceção de segunda chance, o `IDebugExceptionEvent2` evento será enviado para o SDM. Caso contrário, o DE retoma a execução do programa e o sistema operacional ou o tempo de execução trata a exceção.

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
