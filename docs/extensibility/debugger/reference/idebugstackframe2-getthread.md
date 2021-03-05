---
description: Obtém o thread associado a um quadro de pilha.
title: 'IDebugStackFrame2:: GetThread | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetThread
helpviewer_keywords:
- IDebugStackFrame2::GetThread
ms.assetid: cbeef85b-3dd7-4f97-adc2-c4d197d979fc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 340a43cd79feb491ce6b15a1443b456fd0726c5e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168602"
---
# <a name="idebugstackframe2getthread"></a>IDebugStackFrame2::GetThread
Obtém o thread associado a um quadro de pilha.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetThread ( 
   IDebugThread2** ppThread
);
```

```csharp
int GetThread ( 
   out IDebugThread2 ppThread
);
```

## <a name="parameters"></a>Parâmetros
`ppThread`\
fora Retorna um objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o thread.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
