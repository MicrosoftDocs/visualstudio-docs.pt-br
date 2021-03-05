---
description: Especifica os critérios para comparar dois contextos de documento.
title: DOCCONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f64e2e8ec365daa84cbd1d4f7e3e9bdc43391d5e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170426"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
Especifica os critérios para comparar dois contextos de documento.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="fields"></a>Campos
`DOCCONTEXT_EQUAL`\
Localize o primeiro contexto de documento na lista que é igual ao contexto do documento de destino.

`DOCCONTEXT_LESS_THAN`\
Localize o primeiro contexto do documento na lista que seja menor que o contexto do documento de destino.

`DOCCONTEXT_GREATER_THAN`\
Localize o primeiro contexto de documento na lista que é maior que o contexto do documento de destino.

`DOCCONTEXT_SAME_DOCUMENT`\
Localize o primeiro contexto de documento na lista que está no mesmo documento que o contexto do documento de destino.

## <a name="remarks"></a>Comentários
Passado como um argumento para o método [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md) .

Esses valores são usados para especificar um critério de comparação para localizar o primeiro contexto de documento em uma lista. Um contexto de documento recebe uma lista de contextos de documento para se compará-lo com o `IDebugDocumentContext2::Compare` método. O primeiro contexto de documento na lista para o qual o operador de comparação é `true` retornado.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Comparar](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
