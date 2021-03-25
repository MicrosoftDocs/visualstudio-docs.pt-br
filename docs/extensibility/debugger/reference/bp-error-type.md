---
description: Especifica o tipo de erro de um ponto de interrupção.
title: BP_ERROR_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ddff439aba67248bd2eb706a85c5f91b4bf1628d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085280"
---
# <a name="bp_error_type"></a>BP_ERROR_TYPE
Especifica o tipo de erro de um ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
typedef DWORD BP_ERROR_TYPE;
```

```csharp
public enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
```

## <a name="fields"></a>Campos
`BPET_NONE`\
Não especifica nenhum erro de ponto de interrupção.

`BPET_TYPE_WARNING`\
Especifica um erro de ponto de interrupção de estilo de aviso.

`BPET_TYPE_ERROR`\
Especifica um erro de ponto de interrupção de estilo de erro.

`BPET_SEV_HIGH`\
Especifica um erro de ponto de interrupção de alta severidade.

`BPET_SEV_GENERAL`\
Especifica um erro de ponto de interrupção de severidade média.

`BPET_SEV_LOW`\
Especifica um erro de ponto de interrupção de baixa severidade.

`BPET_TYPE_MASK`\
Especifica um erro de ponto de interrupção de estilo de máscara.

`BPET_SEV_MASK`\
Especifica um erro de ponto de interrupção de estilo de máscara de gravidade.

`BPET_GENERAL_WARNING`\
Especifica um erro de ponto de interrupção de estilo de aviso geral.

`BPET_GENERAL_ERROR`\
Especifica um erro de ponto de interrupção de estilo de erro geral.

`BPET_ALL`\
Especifica todos os tipos de erro de ponto de interrupção.

## <a name="remarks"></a>Comentários
Esses valores podem ser combinados com uma e bit-a-bit `OR` e usados para o `dwType` membro da estrutura de [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) . Passado como um parâmetro para o método [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md) .

Um tipo de erro de ponto de interrupção é composto por um tipo e uma severidade. Isso significa que um tipo de erro de ponto de interrupção nunca é apenas um tipo (por exemplo, `BPET_TYPE_ERROR` ) ou uma severidade (por exemplo, `BPET_SEV_GENERAL` ) por si só. `BPET_GENERAL_WARNING` e `BPET_GENERAL_ERROR` forneça valores predefinidos para avisos gerais e pontos de interrupção de erro.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
