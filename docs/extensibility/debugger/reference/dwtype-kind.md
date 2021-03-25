---
description: Especifica como interpretar o tipo de um objeto IDebugField.
title: dwTYPE_KIND | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- dwTYPE_KIND
helpviewer_keywords:
- dwTYPE_KIND enumeration
ms.assetid: 6ff56b0f-c502-4e6c-9829-bfa05361b783
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 25b7fd89de0af624425767f21b81780459068372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095947"
---
# <a name="dwtype_kind"></a>dwTYPE_KIND
Especifica como interpretar o tipo de um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) .

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};

typedef DWORD dwTYPE_KIND;
```

```csharp
public enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};
```

## <a name="fields"></a>Campos
`TYPE_KIND_METADATA`\
A União de [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) deve ser interpretada como uma estrutura de [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) .

`TYPE_KIND_PDB`\
A `TYPE_INFO` União deve ser interpretada como uma estrutura de [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) .

`TYPE_KIND_BUILT`\
A `TYPE_INFO` União deve ser interpretada como uma estrutura de [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) .

## <a name="remarks"></a>Comentários
Os valores dessa enumeração aparecem no `dwKind` campo da estrutura de [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) e são usados para determinar como interpretar o `type` membro da União. A `TYPE_INFO` estrutura é retornada por uma chamada para o método [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: sh. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
