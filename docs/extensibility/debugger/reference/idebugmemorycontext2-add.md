---
description: Adiciona o valor especificado ao contexto atual e retorna um novo contexto.
title: 'IDebugMemoryContext2:: Add | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59daddd38daff2f04f12bc0d1be4e06ec90cf723
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166418"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
Adiciona o valor especificado ao contexto atual e retorna um novo contexto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>Parâmetros
`dwCount`\
no O valor a ser adicionado ao contexto atual.

`ppMemCxt`\
fora Retorna um novo objeto [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um contexto de memória é um endereço, portanto, a adição de um valor a um endereço produz um novo endereço que requer uma nova interface de contexto.

 Esse método sempre deve produzir um novo contexto, mesmo se o endereço resultante estiver fora do espaço de memória associado a esse contexto. A única exceção a isso é se nenhuma memória puder ser alocada para o novo contexto ou se `ppMemCxt` for um valor nulo (que é um erro).

## <a name="see-also"></a>Confira também
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
