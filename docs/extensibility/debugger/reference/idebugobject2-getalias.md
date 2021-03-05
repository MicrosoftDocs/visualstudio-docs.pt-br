---
description: Obtém o alias associado a este objeto, se houver.
title: 'IDebugObject2:: getalias | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c2ac683a5fb4d694b7cf3ab84849b9d7c7df7a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143123"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
Obtém o alias associado a este objeto, se houver.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>Parâmetros
`ppAlias`\
fora Retorna um objeto [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) que representa o alias para este objeto; caso contrário, retorna um valor nulo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um alias para um objeto é criado com uma chamada para o método [createalias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) .

## <a name="see-also"></a>Confira também
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
