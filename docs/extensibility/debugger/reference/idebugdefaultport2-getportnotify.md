---
description: Esse método obtém uma interface IDebugPortNotify2 para essa porta.
title: 'IDebugDefaultPort2:: GetPortNotify | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8ed43d96a7035dbd9e75a8e64a23e556997e087c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077467"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
Esse método obtém uma interface [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) para essa porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPortNotify(
   IDebugPortNotify2** ppPortNotify
);
```

```csharp
int GetPortNotify(
   out IDebugPortNotify2 ppPortNotify
);
```

## <a name="parameters"></a>Parâmetros
`ppPortNotify`\
fora Um objeto [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Normalmente, o `QueryInterface` método é chamado no objeto que implementa a interface [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) para obter uma interface [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) . No entanto, há circunstâncias em que a interface desejada é implementada em um objeto diferente. Esse método oculta essas circunstâncias e retorna a `IDebugPortNotify2` interface do objeto mais apropriado.

## <a name="see-also"></a>Confira também
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
