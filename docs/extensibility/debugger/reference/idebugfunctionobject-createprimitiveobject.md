---
description: Cria um objeto de dados primitivo, como um inteiro simples.
title: 'IDebugFunctionObject:: createprimitivaobject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c706d8908f1fa8776d1d7304772a0c5eec03bd2d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073489"
---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
Cria um objeto de dados primitivo, como um inteiro simples.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreatePrimitiveObject( 
   OBJECT_TYPE    ot,
   IDebugObject** ppObject
);
```

```csharp
int CreatePrimitiveObject(
   enum_OBJECT_TYPE ot,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>Parâmetros
`ot`\
no Um valor da enumeração de [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) que representa o tipo de primitiva a ser criado.

`ppObject`\
fora Retorna um [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o objeto recém-criado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Chame esse método para criar um objeto que representa um objeto primitivo que é um parâmetro para a função que é representada pela interface [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) . Por exemplo, se a cadeia de caracteres de expressão for "myString (5)", esse método seria usado para criar um objeto que representa o inteiro 5.

## <a name="see-also"></a>Confira também
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
