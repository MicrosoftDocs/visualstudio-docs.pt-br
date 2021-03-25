---
description: Retorna o próximo conjunto de elementos da enumeração de portas.
title: 'IEnumDebugPorts2:: Next | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Next
helpviewer_keywords:
- IEnumDebugPorts2::Next
ms.assetid: 3f43d18c-6bd1-4ddd-95ef-9550abd2ad09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e5972a5676c0e7859886578cb871c9a25846a4dc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052808"
---
# <a name="ienumdebugports2next"></a>IEnumDebugPorts2::Next
Retorna o próximo conjunto de elementos da enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Next(
   ULONG         celt,
   IDebugPort2** rgelt,
   ULONG*        pceltFetched
);
```

```csharp
int Next(
   uint          celt,
   IDebugPort2[] rgelt,
   ref uint      pceltFetched
);
```

## <a name="parameters"></a>Parâmetros
`celt`\
no O número de elementos a serem recuperados. Também especifica o tamanho máximo da `rgelt` matriz.

`rgelt`\
[entrada, saída] Matriz de elementos [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) a ser preenchida.

`pceltFetched`\
fora Retorna o número de elementos realmente retornados em `rgelt` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se menos do que o número solicitado de elementos puder ser retornado; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
