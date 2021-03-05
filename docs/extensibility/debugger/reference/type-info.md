---
description: Essa estrutura especifica vários tipos de informações sobre o tipo de um campo.
title: TYPE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e6b37fbc4d2d812bfa10d8f05455050bb5a239d
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223414"
---
# <a name="type_info"></a>TYPE_INFO
Essa estrutura especifica vários tipos de informações sobre o tipo de um campo.

## <a name="syntax"></a>Sintaxe

```cpp
struct _tagTYPE_INFO_UNION {
   dwTYPE_KIND dwKind;
   union {
      METADATA_TYPE typeMeta;
      PDB_TYPE      typePdb;
      BUILT_TYPE    typeBuilt;
      DWORD         unused;
   } type;
} TYPE_INFO;
```

```csharp
public struct TYPE_INFO {
   public uint   dwKind;
   public IntPtr unionmember;
};
```

## <a name="members"></a>Membros
 `dwKind`\
 Um valor da enumeração [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) que determina como interpretar a União.

 `type.typeMeta`\
 [Somente C++] Contém uma estrutura de [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) se `dwKind` for `TYPE_KIND_METADATA` .

 `type.typePdb`\
 [Somente C++] Contém uma estrutura de [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) se `dwKind` for `TYPE_KIND_PDB` .

 `type.typeBuilt`\
 [Somente C++] Contém uma estrutura de [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) se `dwKind` for `TYPE_KIND_BUILT` .

 `type.unused`\
 Preenchimento não usado.

 `type`\
 Nome da União.

 `unionmember`\
 [Somente C#] Realize o marshaling para o tipo de estrutura apropriado com base em `dwKind` .

## <a name="remarks"></a>Comentários
 Essa estrutura é passada para o método [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) onde está preenchida. Como o conteúdo da estrutura é interpretado baseia-se no `dwKind` campo.

> [!NOTE]
> [Somente C++] Se for `dwKind` igual a `TYPE_KIND_BUILT` , será necessário liberar o objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) subjacente ao destruir a `TYPE_INFO` estrutura. Isso é feito chamando `typeInfo.type.typeBuilt.pUnderlyingField->Release()`.

 [Somente C#] A tabela a seguir mostra como interpretar o `unionmember` membro para cada tipo de tipo. O exemplo mostra como isso é feito para um tipo de tipo.

|`dwKind`|`unionmember` interpretado como|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>Exemplo
 Este exemplo mostra como interpretar o `unionmember` membro da `TYPE_INFO` estrutura em C#. Este exemplo mostra a interpretação de apenas um tipo ( `TYPE_KIND_METADATA` ), mas os outros são interpretados exatamente da mesma maneira.

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(TYPE_INFO ti)
        {
            if (ti.dwKind == (uint)enum_dwTypeKind.TYPE_KIND_METADATA)
            {
                 METADATA_TYPE dataType = (METADATA_TYPE)Marshal.PtrToStructure(ti.unionmember,
                                               typeof(METADATA_TYPE));
            }
        }
    }
}
```

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
