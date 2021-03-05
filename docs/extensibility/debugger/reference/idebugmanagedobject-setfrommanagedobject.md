---
description: Define o valor da instância do objeto de classe de valor da instância da classe de valor fornecida como um parâmetro.
title: 'IDebugManagedObject:: SetFromManagedObject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::SetFromManagedObject
helpviewer_keywords:
- IDebugManagedObject::SetFromManagedObject method
ms.assetid: 8700ee8d-2704-4580-bccc-046837a24edd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b4038b4f3560b7cd526261f898c01f384421f42
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165209"
---
# <a name="idebugmanagedobjectsetfrommanagedobject"></a>IDebugManagedObject::SetFromManagedObject
Define o valor da instância do objeto de classe de valor da instância da classe de valor fornecida como um parâmetro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetFromManagedObject( 
   IUnknown* pManagedObject
);
```

```csharp
int SetFromManagedObject(
   object pManagedObject
);
```

## <a name="parameters"></a>Parâmetros
`pManagedObject`\
no Uma interface que representa o objeto gerenciado que contém o novo valor.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é usado para alterar o objeto gerenciado, conforme representado pelo objeto [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) .

## <a name="see-also"></a>Confira também
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
