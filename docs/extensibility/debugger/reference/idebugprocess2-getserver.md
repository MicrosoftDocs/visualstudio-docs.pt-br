---
description: Obtém o servidor em que esse processo está sendo executado.
title: 'IDebugProcess2:: GetServer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetServer
helpviewer_keywords:
- IDebugProcess2::GetServer
ms.assetid: 8f73c530-cceb-4f1f-8c63-1cc0ccd4a310
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fba7af19093d853d227241187242a24bf9bd8cdb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169191"
---
# <a name="idebugprocess2getserver"></a>IDebugProcess2::GetServer
Obtém o servidor em que esse processo está sendo executado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetServer( 
   IDebugCoreServer2** ppServer
);
```

```csharp
int GetServer( 
   out IDebugCoreServer2 ppServer
);
```

## <a name="parameters"></a>Parâmetros
`ppServer`\
fora Retorna um objeto [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) que representa o servidor no qual esse processo está em execução.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Mais de um servidor pode ser executado em um único computador.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
