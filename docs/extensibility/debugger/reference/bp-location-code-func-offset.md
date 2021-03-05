---
description: Descreve o local de deslocamento de um ponto de interrupção em uma função no código.
title: BP_LOCATION_CODE_FUNC_OFFSET | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET
helpviewer_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET structure
ms.assetid: ab38f7ca-fa01-4cf3-a06c-56cbb7207617
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 83a5a27601ab6d7498394d6723b86ad3e66aceb5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144358"
---
# <a name="bp_location_code_func_offset"></a>BP_LOCATION_CODE_FUNC_OFFSET
Descreve o local de deslocamento de um ponto de interrupção em uma função no código.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _BP_LOCATION_CODE_FUNC_OFFSET {
    BSTR                     bstrContext;
    IDebugFunctionPosition2* pFuncPos;
} BP_LOCATION_CODE_FUNC_OFFSET;
```

## <a name="members"></a>Membros
`bstrContext`\
O contexto do ponto de interrupção, normalmente um nome de método ou função, como visto em uma pilha de chamadas.

`pFuncPos`\
O objeto [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md) que descreve o nome da função e a posição relativa do início da função.

## <a name="remarks"></a>Comentários
Essa estrutura é um membro da estrutura de [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) como parte de uma União.

O `pFuncPos` membro indica onde definir o ponto de interrupção da função.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)
