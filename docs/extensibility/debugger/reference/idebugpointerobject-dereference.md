---
description: Obtém o objeto apontado para.
title: IDebugPointerObject::D eReference | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::Dereference
helpviewer_keywords:
- IDebugPointerObject::Dereference method
ms.assetid: 196ec2cc-8569-4780-b217-23b24e7f50ca
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e4aa96f726ec18e84aceba159fe9be6128456ce0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169685"
---
# <a name="idebugpointerobjectdereference"></a>IDebugPointerObject::Dereference
Obtém o objeto apontado para.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DeReference( 
   DWORD          dwIndex,
   IDebugObject** ppObject
);
```

```csharp
int Dereference(
   uint             dwIndex,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>Parâmetros
`dwIndex`\
no Um deslocamento de byte simples do início do objeto apontado para.

`ppObject`\
fora Retorna um objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o objeto apontado para, além de offset, se houver.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro. Retorna E_FAIL se esse objeto não apontar para outro objeto.

## <a name="remarks"></a>Comentários
 O objeto apontado pode ser um tipo primitivo ou mais complexo, como uma classe ou estrutura.

## <a name="see-also"></a>Confira também
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
