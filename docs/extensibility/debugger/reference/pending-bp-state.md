---
description: Especifica o estado de um ponto de interrupção pendente (um ponto de interrupção que ainda não foi associado).
title: PENDING_BP_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE
helpviewer_keywords:
- PENDING_BP_STATE enumeration
ms.assetid: ac04ad72-fa92-4a15-ade2-0d0bbbadfc7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d041042be92fe68dd6f0ea35bbdb4f6dd6d9ac7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086372"
---
# <a name="pending_bp_state"></a>PENDING_BP_STATE
Especifica o estado de um ponto de interrupção pendente (um ponto de interrupção que ainda não foi associado).

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
typedef DWORD PENDING_BP_STATE;
```

```csharp
public enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>Campos
 `PBPS_NONE`\
 Espaço reservado para zero. Esse valor nunca é retornado.

 `PBPS_DELETED`\
 Indica que o ponto de interrupção pendente foi excluído.

 `PBPS_DISABLED`\
 Indica que o ponto de interrupção pendente está desabilitado.

 `PBPS_ENABLED`\
 Indica que o ponto de interrupção pendente está habilitado.

## <a name="remarks"></a>Comentários
 Use como o `state` membro da estrutura de [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)
