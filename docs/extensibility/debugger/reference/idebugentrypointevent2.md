---
title: IDebugEntryPointEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEntryPointEvent2
helpviewer_keywords:
- IDebugEntryPointEvent2 interface
ms.assetid: a15d1cc3-97b7-438c-8d24-c23149708f42
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 531ff846f2488193ed7f3d9f200a1a4ea04df6f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730324"
---
# <a name="idebugentrypointevent2"></a>IDebugEntryPointEvent2
O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) quando o programa está prestes a executar sua primeira instrução de código de usuário.

## <a name="syntax"></a>Syntax

```
IDebugEntryPointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface como parte de suas operações normais. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia esse objeto DE evento quando o programa que está sendo depurado é carregado e está pronto para executar a primeira instrução do código do usuário. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado.

## <a name="remarks"></a>Comentários
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) é enviado quando o programa está prestes a executar a primeira instrução. Por exemplo, `IDebugEntryPoint2` é enviado quando o programa está prestes a executar a função do usuário `main` .

 Quando o DE envia `IDebugEntryPointEvent2` , a posição atual do código deve estar na primeira instrução do código do usuário, como `main` .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
