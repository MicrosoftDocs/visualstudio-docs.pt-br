---
description: Ignora o número especificado de elementos de DEBUG_PROPERTY_INFO.
title: 'IEnumDebugPropertyInfo2:: Skip | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2::Skip
helpviewer_keywords:
- IEnumDebugPropertyInfo2::Skip
ms.assetid: 0366c778-18eb-4065-a452-64b70c751a58
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 799aadf40eafa03e944e5e25f9c721b459320c8c
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225962"
---
# <a name="ienumdebugpropertyinfo2skip"></a>IEnumDebugPropertyInfo2::Skip
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
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
