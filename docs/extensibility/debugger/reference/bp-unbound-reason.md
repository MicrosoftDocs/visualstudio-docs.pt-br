---
description: Fornece o motivo pelo qual um ponto de interrupção foi desassociado.
title: BP_UNBOUND_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13f723c6395b8b271d6f097d811c5a31569c5853
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067693"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
Fornece o motivo pelo qual um ponto de interrupção foi desassociado.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
typedef DWORD BP_UNBOUND_REASON;
```

```csharp
public enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
```

## <a name="fields"></a>Campos
`BPUR_UNKNOWN`\
O motivo é desconhecido.

`BPUR_CODE_UNLOADED`\
O código que contém o ponto de interrupção foi descarregado.

`BPUR_BREAKPOINT_REBIND`\
O ponto de interrupção foi reassociado a um local diferente. Isso pode acontecer após as operações de editar e continuar quando o ponto de interrupção se move, ou quando o ponto de interrupção está associado a um arquivo com um caminho que não é mais válido.

`BPUR_ BREAKPOINT_ERROR`\
O ponto de interrupção é determinado como erro depois de ser associado. Isso ocorre com pontos de interrupção gerenciados cujas condições não são mais válidas.

## <a name="remarks"></a>Comentários
Retornado pelo método [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)
