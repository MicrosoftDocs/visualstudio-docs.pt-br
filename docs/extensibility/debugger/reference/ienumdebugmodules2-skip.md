---
description: Ignora o número especificado de elementos na enumeração modules.
title: 'IEnumDebugModules2:: Skip | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Skip
helpviewer_keywords:
- IEnumDebugModules2::Skip
ms.assetid: 61dc42f4-8544-45bb-8da0-fb22cccec7da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ee6094852dc9a58d7f976d9fd58de62e9b89cea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086502"
---
# <a name="ienumdebugmodules2skip"></a>IEnumDebugModules2::Skip
Ignora o número especificado de elementos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>Parâmetros
`celt`\
no Número de elementos a serem ignorados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se `celt` é maior que o número de elementos restantes; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se `celt` o especificar um valor maior que o número de elementos restantes, a enumeração será definida como end e `S_FALSE` será retornada.

## <a name="see-also"></a>Confira também
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
