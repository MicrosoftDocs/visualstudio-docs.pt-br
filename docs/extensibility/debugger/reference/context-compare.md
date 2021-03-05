---
description: Especifica os critérios para comparar dois contextos de memória.
title: CONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 70f4621eaad5e494684e6c227959e13566a22eba
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170777"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
Especifica os critérios para comparar dois contextos de memória.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
typedef DWORD CONTEXT_COMPARE;
```

```csharp
public enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
```

## <a name="fields"></a>Campos
`CONTEXT_EQUAL`\
Localize o primeiro contexto de memória na lista que é igual ao contexto de memória de destino.

`CONTEXT_LESS_THAN`\
Localize o primeiro contexto de memória na lista que seja menor que o contexto de memória de destino.

`CONTEXT_GREATER_THAN`\
Localize o primeiro contexto de memória na lista que é maior que o contexto de memória de destino.

`CONTEXT_LESS_THAN_OR_EQUAL`\
Localize o primeiro contexto de memória na lista que seja menor ou igual ao contexto de memória de destino.

`CONTEXT_GREATER_THAN_OR_EQUAL`\
Localize o primeiro contexto de memória na lista que seja maior ou igual ao contexto de memória de destino.

`CONTEXT_SAME_SCOPE`\
Localize o primeiro contexto de memória na lista que está no mesmo escopo que o contexto de memória de destino.

`CONTEXT_SAME_FUNCTION`\
Localize o primeiro contexto de memória na lista que está na mesma função que o escopo de memória de destino.

`CONTEXT_SAME_MODULE`\
Localize o primeiro contexto de memória na lista que está no mesmo módulo que o contexto de memória de destino.

`CONTEXT_SAME_PROCESS`\
Localize o primeiro contexto de memória na lista que está no mesmo processo que o contexto de memória de destino.

## <a name="remarks"></a>Comentários
Passado como um argumento para o método [Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md) .

Esses valores são usados para localizar o primeiro contexto de memória em uma lista que satisfaça os critérios de comparação especificados. Um contexto de memória recebe uma lista de contextos de memória para se compará-lo com o `IDebugMemoryContext2::Compare` método. O primeiro contexto de memória na lista para o qual o operador de comparação é `true` retornado.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Comparar](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
