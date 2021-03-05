---
description: Retorna o próximo conjunto de elementos da enumeração de caminhos de código.
title: 'IEnumCodePaths2:: Next | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2::Next
helpviewer_keywords:
- IEnumCodePaths2::Next
ms.assetid: c7a8fe97-2abc-4cee-8aef-64f1daa93b5c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7782a2b962786b191849dbdc1a9a7f3f7c727e9f
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222686"
---
# <a name="ienumcodepaths2next"></a>IEnumCodePaths2::Next
Retorna o próximo conjunto de elementos da enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Next(
   ULONG       celt,
   CODE_PATH** rgelt,
   ULONG*      pceltFetched
);
```

```csharp
int Next(
   uint        celt,
   CODE_PATH[] rgelt,
   ref uint    pceltFetched
);
```

## <a name="parameters"></a>Parâmetros
`celt`\
no O número de elementos a serem recuperados. Também especifica o tamanho máximo da `rgelt` matriz.

`rgelt`\
[entrada, saída] Matriz de elementos [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) a ser preenchida.

`pceltFetched`\
fora Retorna o número de elementos realmente retornados em `rgelt` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se menos do que o número solicitado de elementos puder ser retornado; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [CODE_PATH](../../../extensibility/debugger/reference/code-path.md)
