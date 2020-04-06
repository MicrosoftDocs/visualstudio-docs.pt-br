---
title: IDebugThread2::GetLogicalThread | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e148fb0b9b043fc1717effca00d698ee14beb2f1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718845"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
Os motores de depuração não implementam este método.

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

## <a name="parameters"></a>parâmetros
`pStackFrame`\
[em] Um objeto [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que representa o quadro stack.

`ppLogicalThread`\
[fora] Retorna `IDebugLogicalThread2` uma interface que representa o segmento lógico associado. Uma implementação do mecanismo de depuração deve definir isso como um valor nulo.

## <a name="return-value"></a>Valor retornado
 As implementações do `E_NOTIMPL`mecanismo de depuração sempre retornam .

## <a name="see-also"></a>Confira também
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
