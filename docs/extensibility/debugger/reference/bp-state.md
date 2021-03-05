---
description: Especifica a existência de um ponto de interrupção associado e também especifica se ele está habilitado.
title: BP_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_STATE
helpviewer_keywords:
- BP_STATE enumeration
ms.assetid: 08aa6a3f-3e5f-4c83-8eca-7b7b5f8e208d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ae225a7eeb782257a716c48c1882d78ad150e7e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168329"
---
# <a name="bp_state"></a>BP_STATE
Especifica a existência de um ponto de interrupção associado e também especifica se ele está habilitado.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
typedef DWORD BP_STATE;
```

```csharp
public enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>Campos
`BPS_NONE`\
Especifica que não existe nenhum ponto de interrupção.

`BPS_DELETED`\
Especifica que o ponto de interrupção foi excluído.

`BPS_DISABLED`\
Especifica que o ponto de interrupção está desabilitado.

`BPS_ENABLED`\
Especifica que o ponto de interrupção está habilitado.

## <a name="remarks"></a>Comentários
Retornado do método [GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)
