---
description: Especifica a estrutura do local de resolução do ponto de interrupção.
title: BP_RESOLUTION_LOCATION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_LOCATION
helpviewer_keywords:
- BP_RESOLUTION_LOCATION structure
ms.assetid: 21dc5246-69c1-43e3-855c-9cd4e596c0e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aefbb27a7eb693ceef3bd64afb610607697ac23e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089115"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
Especifica a estrutura do local de resolução do ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```cpp
struct _BP_RESOLUTION_LOCATION {
    BP_TYPE bpType;
    union {
        BP_RESOLUTION_CODE bpresCode;
        BP_RESOLUTION_DATA bpresData;
        int                unused;
    } bpResLocation;
} BP_RESOLUTION_LOCATION;
```

```csharp
public struct BP_RESOLUTION_LOCATION {
    public uint   bpType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public uint   unionmember4;
};
```

## <a name="members"></a>Membros
`bpType`\
Um valor da enumeração [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) que especifica como interpretar a `bpResLocation` União ou `unionmemberX` os membros.

`bpResLocation.bpresCode`\
[Somente C++] Contém a estrutura de [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md) se `bpType`  =  `BPT_CODE` .

`bpResLocation.bpresData`\
[Somente C++] Contém a estrutura de [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md) se `bpType`  =  `BPT_DATA` .

`bpResLocation.unused`\
[Somente C++] Um espaço reservado.

`unionmember1`\
[Somente C#] Consulte comentários sobre como interpretar.

`unionmember2`\
[Somente C#] Consulte comentários sobre como interpretar.

`unionmember3`\
[Somente C#] Consulte comentários sobre como interpretar.

`unionmember4`\
[Somente C#] Consulte comentários sobre como interpretar.

## <a name="remarks"></a>Comentários
Essa estrutura é um membro das estruturas [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) e [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) .

 [Somente C#] Os `unionmemberX` Membros são interpretados de acordo com a tabela a seguir. Examine a coluna à esquerda do `bpType` valor e, em seguida, para determinar o que cada `unionmemberX` membro representa e empacotar de `unionmemberX` acordo. Consulte o exemplo de uma maneira de interpretar essa estrutura em C#.

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPT_DATA`|`string` (expressão de dados)|`string` (nome da função)|`string` (nome da imagem)|`enum_BP_RES_DATA_FLAGS`|

## <a name="example"></a>Exemplo
Este exemplo mostra como interpretar a `BP_RESOLUTION_LOCATION` estrutura em C#.

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_RESOLUTION_LOCATION bprl)
        {
            if (bprl.bpType == (uint)enum_BP_TYPE.BPT_CODE)
            {
                IDebugCodeContext2 pContext = (IDebugCodeContext2)Marshal.GetObjectForIUnknown(bp.unionmember1);
            }
            else if (bprl.bpType == (uint)enum_BP_TYPE.BPT_DATA)
            {
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                string functionName = Marshal.PtrToStringBSTR(bp.unionmember2);
                string imageName = Marshal.PtrToStringBSTR(bp.unionmember3);
                enum_BP_RES_DATA_FLAGS numElements = (enum_BP_RES_DATA_FLAGS)bp.unionmember4;
            }
        }
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
