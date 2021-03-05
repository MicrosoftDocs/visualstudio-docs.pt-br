---
description: Determina se o objeto representa dados do usuário.
title: 'IDebugObject2:: isuserdata | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsUserData
helpviewer_keywords:
- IDebugObject2::IsUserData method
ms.assetid: 6ffa0d0e-f742-496d-acc7-db74c248bc45
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b9264ed546a4f1c9abcf42b1376e0b21b0f27940
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169983"
---
# <a name="idebugobject2isuserdata"></a>IDebugObject2::IsUserData
Determina se o objeto representa dados do usuário.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT IsUserData(
   BOOL* pfUser
);
```

```csharp
int IsUserData(
   out int pfUser
);
```

## <a name="parameters"></a>Parâmetros
`pfUser`\
fora Retorna zero ( `TRUE` ) se o objeto representar dados do usuário; zero ( `FALSE` ) se não tiver.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Os dados do usuário são qualquer objeto que faça parte de um módulo designado como JustMyCode (uma opção configurável pelo usuário que marca um módulo como código do usuário e, portanto, visível em um rastreamento de pilha).

## <a name="see-also"></a>Confira também
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
