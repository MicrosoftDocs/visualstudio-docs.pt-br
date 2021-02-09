---
title: IDebugInterceptExceptionCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2
ms.assetid: 8ebc256b-5428-4ed6-a505-6aedc8242b8e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d98f8653d851eb338a96f969d73a2514b555f400
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890273"
---
# <a name="idebuginterceptexceptioncompleteevent2"></a>IDebugInterceptExceptionCompleteEvent2
Essa interface é enviada pelo mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando o DE tiver concluído o tratamento de um evento interceptado.

## <a name="syntax"></a>Sintaxe

```
IDebugInterceptExceptionCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para relatar que o processamento de uma exceção interceptada foi concluído. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para relatar a conclusão de uma exceção interceptada. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A `IDebugInterceptExceptionCompleteEvent2` interface implementa os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[GetInterceptCookie](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2-getinterceptcookie.md)|Retorna o valor exclusivo associado à exceção manipulada.|

## <a name="remarks"></a>Comentários
 Esse evento será enviado por [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) quando esse método tiver concluído com êxito o tratamento de uma exceção interceptada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
