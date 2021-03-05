---
description: Esse método obtém uma interface para o servidor no qual essa porta está.
title: 'IDebugDefaultPort2:: GetServer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d5bfd242cd3f441bf094f94e41a78e240f1ec46
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162973"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
Esse método obtém uma interface para o servidor no qual essa porta está.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetServer(
   IDebugCoreServer3** ppServer
);
```

```csharp
int GetServer(
   out IDebugCoreServer3 ppServer
);
```

## <a name="parameters"></a>Parâmetros
`ppServer`\
fora Retorna um objeto que implementa a interface [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) é implementado pelo Visual Studio e representa o servidor no qual a porta está localizada.

## <a name="see-also"></a>Confira também
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
