---
description: Cria um objeto de cadeia de caracteres.
title: 'IDebugFunctionObject:: createstringobject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateStringObject
helpviewer_keywords:
- IDebugFunctionObject::CreateStringObject method
ms.assetid: fd6070ab-07d4-4ea1-8d71-b16592d6f1a7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 15ad52d990492d7f78f3f8246e786dc0b037e23f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072891"
---
# <a name="idebugfunctionobjectcreatestringobject"></a>IDebugFunctionObject::CreateStringObject
Cria um objeto de cadeia de caracteres.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreateStringObject( 
   LPCOLESTR      pcstrString,
   IDebugObject** ppObject
);
```

```csharp
int CreateStringObject(
   string      pcstrString,
   out IDebugObject ppOjbect
);
```

## <a name="parameters"></a>Parâmetros
`pcstrString`\
no O valor da cadeia de caracteres para o objeto de cadeia de caracteres.

`ppObject`\
fora Retorna um objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o objeto de cadeia de caracteres recém-criado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Chame esse método para criar um objeto que representa uma cadeia de caracteres que é um parâmetro para a função que é representada pela interface [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) .

## <a name="see-also"></a>Confira também
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
