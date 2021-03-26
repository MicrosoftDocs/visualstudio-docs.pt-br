---
description: Cria uma cópia do objeto gerenciado no espaço de endereço do mecanismo de depuração.
title: 'IDebugObject:: GetManagedDebugObject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 56961930e08e7d53dfe387c00642ae7266c230c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081913"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
Cria uma cópia do objeto gerenciado no espaço de endereço do mecanismo de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetManagedDebugObject( 
   IDebugManagedObject** ppObject
);
```

```csharp
int GetManagedDebugObject(
   out IDebugManagedObject ppObject
);
```

## <a name="parameters"></a>Parâmetros
`ppObject`\
fora Retorna um objeto [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) que representa o objeto gerenciado recém-criado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro. Retorna E_FAIL se esse [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) não representar uma instância de classe de valor gerenciado.

## <a name="remarks"></a>Comentários
 Esse objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) deve representar uma instância de classe de valor gerenciado, como uma `System.Decimal` instância. Com uma cópia local, a sobrecarga de chamar [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) é eliminada.

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
