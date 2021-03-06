---
description: A estrutura de BUILT_TYPE especifica informações sobre um tipo de campo extraído dos metadados.
title: BUILT_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00a031d02bba7ffcc1dca6f2cf73cfceeed04838
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096571"
---
# <a name="built_type"></a>BUILT_TYPE
Essa estrutura especifica informações sobre um tipo de campo extraído dos metadados.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagTYPE_BUILT {
    ULONG32      ulAppDomainID;
    GUID         guidModule;
    IDebugField* pUnderlyingField;
} BUILT_TYPE;
```

```csharp
public struct BUILT_TYPE {
    public uint        ulAppDomainID;
    public Guid        guidModule;
    public IDebugField pUnderlyingField;
};
```

## <a name="members"></a>Membros
`ulAppDomainID`\
ID do aplicativo do qual o símbolo veio. Isso é usado para identificar exclusivamente uma instância do aplicativo.

`guidModule`\
O GUID do módulo que contém este campo.

`pUnderlyingField`\
Um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que identifica o campo subjacente associado a este campo interno.

## <a name="remarks"></a>Comentários
Essa estrutura aparece como parte da União na estrutura [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) quando o `dwKind` campo da `TYPE_INFO` estrutura é definido como `TYPE_KIND_BUILT` (um valor da enumeração [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) ).

## <a name="requirements"></a>Requisitos
Cabeçalho: sh. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
