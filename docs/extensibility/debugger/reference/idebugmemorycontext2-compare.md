---
description: Compara o contexto de memória a cada contexto na matriz especificada da maneira indicada por sinalizadores de comparação, retornando um índice do primeiro contexto que corresponde.
title: 'IDebugMemoryContext2:: Compare | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67acecafd677d5096e1bf975f85e21a5c6cbe133
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076765"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
Compara o contexto de memória a cada contexto na matriz especificada da maneira indicada por sinalizadores de comparação, retornando um índice do primeiro contexto que corresponde.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Compare( 
   CONTEXT_COMPARE        compare,
   IDebugMemoryContext2** rgpMemoryContextSet,
   DWORD                  dwMemoryContextSetLen,
   DWORD*                 pdwMemoryContext
);
```

```csharp
int Compare(
   enum_CONTEXT_COMPARE   compare,
   IDebugMemoryContext2[] rgpMemoryContextSet,
   uint                   dwMemoryContextSetLen,
   out uint               pdwMemoryContext
);
```

## <a name="parameters"></a>Parâmetros
`compare`\
no Um valor da enumeração [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md) que determina o tipo de comparação.

`rgpMemoryContextSet`\
no Uma matriz de referências aos objetos [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) para comparação.

`dwMemoryContextSetLen`\
no O número de contextos na `rgpMemoryContextSet` matriz.

`pdwMemoryContext`\
fora Retorna o índice do primeiro contexto de memória que satisfaz a comparação.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_COMPARE_CANNOT_COMPARE` se os dois contextos não puderem ser comparados.

## <a name="remarks"></a>Comentários
 Um mecanismo de depuração (de) não precisa dar suporte a todos os tipos de comparações, mas deve oferecer suporte a pelo menos `CONTEXT_EQUAL` , `CONTEXT_LESS_THAN` `CONTEXT_GREATER_THAN` e `CONTEXT_SAME_SCOPE` .

## <a name="see-also"></a>Confira também
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
