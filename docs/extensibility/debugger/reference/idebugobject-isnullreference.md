---
description: Testa se este objeto é uma referência nula.
title: 'IDebugObject:: IsNullReference | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsNullReference
helpviewer_keywords:
- IDebugObject::IsNullReference method
ms.assetid: 6dbfcdb0-954f-4486-8fac-7ea8d003e3a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba037f995c97a3bfbf059f51bfb4f8777803a172
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054069"
---
# <a name="idebugobjectisnullreference"></a>IDebugObject::IsNullReference
Testa se este objeto é uma referência nula.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT IsNullReference( 
   BOOL* pfIsNull
);
```

```csharp
int IsNullReference(
   out int pfIsNull
);
```

## <a name="parameters"></a>Parâmetros
`pfIsNull`\
fora Retornará um valor diferente de zero ( `TRUE` ) se esse objeto for uma referência nula; caso contrário, retornará zero ( `FALSE` ).

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Uma referência nula significa um objeto vazio ou um objeto que não foi atribuído ao.

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
