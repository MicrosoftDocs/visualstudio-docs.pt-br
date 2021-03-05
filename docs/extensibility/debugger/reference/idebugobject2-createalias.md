---
description: Cria uma ID exclusiva ou um alias para esse objeto ou retorna um alias existente.
title: 'IDebugObject2:: createalias | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::CreateAlias
helpviewer_keywords:
- IDebugObject2::CreateAlias method
ms.assetid: 54a05920-5d13-4f67-962b-d1a7f013dff9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2c0059b7b3b12b8e2e59524939c4a47aad97219
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170179"
---
# <a name="idebugobject2createalias"></a>IDebugObject2::CreateAlias
Cria uma ID exclusiva ou um alias para esse objeto ou retorna um alias existente.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreateAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int CreateAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>Parâmetros
`ppAlias`\
fora O novo (ou existente) alias.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um alias é um rótulo que representa um objeto específico enquanto o objeto está na memória.

## <a name="see-also"></a>Confira também
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
