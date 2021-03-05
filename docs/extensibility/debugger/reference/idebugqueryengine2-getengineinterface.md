---
description: Obtém uma interface do mecanismo DE depuração personalizado (DE).
title: 'IDebugQueryEngine2:: GetEngineInterface | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cbf727de01c8cbf34d645aff4e0a64aeb476ebbd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167835"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
Obtém uma interface do mecanismo DE depuração personalizado (DE).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEngineInterface( 
   IUnknown** ppUnk
);
```

```csharp
int GetEngineInterface( 
   out object ppUnk
);
```

## <a name="parameters"></a>Parâmetros
`ppUnk`\
fora Retorna um `IUnknown` objeto que representa o mecanismo de depuração (de) e que pode ser consultado para qualquer outra interface válida associada a um de (por exemplo, [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) ou [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)).

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A interface resultante deve ser usada com cuidado porque a chamada por meio de interfaces recuperadas desse método evita o processamento do Gerenciador de depuração de sessão e pode resultar no SDM entrar em um estado insatisfatório ou gerar erros durante a depuração.

## <a name="see-also"></a>Confira também
- [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
