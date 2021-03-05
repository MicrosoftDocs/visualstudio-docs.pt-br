---
description: Os mecanismos de depuração não implementam esse método.
title: 'IDebugThread2:: GetLogicalThread | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9193cde20ba1035552451143c676aab291d7c684
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168342"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
Os mecanismos de depuração não implementam esse método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetLogicalThread( 
   IDebugStackFrame2*     pStackFrame,
   IDebugLogicalThread2** ppLogicalThread
);
```

```csharp
int GetLogicalThread( 
   IDebugStackFrame2        pStackFrame,
   out IDebugLogicalThread2 ppLogicalThread
);
```

## <a name="parameters"></a>Parâmetros
`pStackFrame`\
no Um objeto [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que representa o quadro de pilha.

`ppLogicalThread`\
fora Retorna uma `IDebugLogicalThread2` interface que representa o thread lógico associado. Uma implementação do mecanismo de depuração deve definir isso como um valor nulo.

## <a name="return-value"></a>Valor Retornado
 Implementações do mecanismo de depuração sempre retornam `E_NOTIMPL` .

## <a name="see-also"></a>Confira também
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
