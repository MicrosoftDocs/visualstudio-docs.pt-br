---
title: BP_RESOLUTION_CODE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_CODE
helpviewer_keywords:
- BP_RESOLUTION_CODE structure
ms.assetid: ac103ec5-771c-4667-92de-b5abb53bbb52
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f888c5cbee5747562af070d310a9ca5d8eea913
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901964"
---
# <a name="bp_resolution_code"></a>BP_RESOLUTION_CODE
Descreve o local de um ponto de interrupção de código.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _BP_RESOLUTION_CODE {
    IDebugCodeContext2* pCodeContext;
} BP_RESOLUTION_CODE;
```

```csharp
public struct BP_RESOLUTION_CODE {
    public IDebugCodeContext2 pCodeContext;
};
```

## <a name="members"></a>Membros
`pCodeContext`\
O objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que identifica a posição do ponto de interrupção no código.

## <a name="remarks"></a>Comentários
Essa estrutura é um membro da estrutura de [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) , que, por sua vez, é um membro da estrutura de [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) retornada pelo método [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
