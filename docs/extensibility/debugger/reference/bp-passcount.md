---
title: BP_PASSCOUNT | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e3177ff093aea9a6f52465bd606b22883249d6b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737905"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
Descreve a contagem e as condições nas quais um ponto de interrupção condicional é acionado.

## <a name="syntax"></a>Syntax

```cpp
typedef struct _BP_PASSCOUNT {
    DWORD              dwPassCount;
    BP_PASSCOUNT_STYLE stylePassCount;
} BP_PASSCOUNT;
```

```csharp
public struct BP_PASSCOUNT {
    public uint dwPassCount;
    public uint stylePassCount;
};
```

## <a name="members"></a>Membros
`dwPassCount`\
O número de vezes para passar o ponto de interrupção antes de acionar.

`stylePassCount`\
Um valor da enumeração de [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md) que especifica o estilo da contagem de aprovações de ponto de interrupção.

## <a name="remarks"></a>Comentários
Essa estrutura é membro da estrutura de [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) .

Essa estrutura também é passada como um parâmetro para os métodos[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) e[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)
