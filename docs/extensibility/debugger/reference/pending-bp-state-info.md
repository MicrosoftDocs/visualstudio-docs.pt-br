---
description: Contém informações sobre o estado de um ponto de interrupção que está pronto para ser associado a um local de código.
title: PENDING_BP_STATE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE_INFO
helpviewer_keywords:
- PENDING_BP_STATE_INFO structure
ms.assetid: 4d73ceff-43f9-4e95-8dba-88e1fab2def3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a4da8892239740c65e1fcbbe618fa1ea76183e96
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079677"
---
# <a name="pending_bp_state_info"></a>PENDING_BP_STATE_INFO
Contém informações sobre o estado de um ponto de interrupção que está pronto para ser associado a um local de código.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagPENDING_BP_STATE_INFO { 
   PENDING_BP_STATE       state;
   PENDING_BP_STATE_FLAGS flags;
} PENDING_BP_STATE_INFO;
```

```csharp
public struct PENDING_BP_STATE_INFO { 
   public uint state;
   public uint flags;
};
```

## <a name="members"></a>Membros
 `state`\
 Um valor da enumeração [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md) que especifica o estado do ponto de interrupção pendente.

 `flags`\
 Uma combinação de sinalizadores da enumeração [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md) que especifica se o ponto de interrupção é virtualizado.

## <a name="remarks"></a>Comentários
 Essa estrutura é passada para o método [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md) onde está preenchida.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)
- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)
- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)
