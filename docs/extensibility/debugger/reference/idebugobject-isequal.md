---
description: Compara um objeto com este objeto.
title: 'IDebugObject:: IsEqual | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0907b72f2a0647fc6ff6181ecdc5c7fd8c2134cb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151656"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
Compara um objeto com este objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>Parâmetros
`pObject`\
no Um objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o objeto a ser comparado.

`pfIsEqual`\
fora Retornará um valor diferente de zero ( `TRUE` ) se os valores dos objetos forem iguais; caso contrário, retornará zero ( `FALSE` ).

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Normalmente, esse método pode comparar os endereços dos valores representados pelo `pObject` parâmetro e esse objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) ; se os endereços forem iguais, os objetos poderão ser considerados iguais.

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
