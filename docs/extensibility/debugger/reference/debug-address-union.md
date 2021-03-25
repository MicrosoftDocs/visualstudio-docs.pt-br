---
description: Descreve os diferentes tipos de endereços.
title: DEBUG_ADDRESS_UNION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 71867a6a2cbaaf87b5b0a66eab5f53826fe47fdf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096428"
---
# <a name="debug_address_union"></a>DEBUG_ADDRESS_UNION
Descreve os diferentes tipos de endereços.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagDEBUG_ADDRESS_UNION {
   ADDRESS_KIND dwKind;
   union {
      NATIVE_ADDRESS                  addrNative;
      UNMANAGED_ADDRESS_THIS_RELATIVE addrThisRel;
      UNMANAGED_ADDRESS_PHYSICAL      addrUPhysical;
      METADATA_ADDRESS_METHOD         addrMethod;
      METADATA_ADDRESS_FIELD          addrField;
      METADATA_ADDRESS_LOCAL          addrLocal;
      METADATA_ADDRESS_PARAM          addrParam;
      METADATA_ADDRESS_ARRAYELEM      addrArrayElem;
      METADATA_ADDRESS_RETVAL         addrRetVal;
      DWORD                           unused;
   } addr;
} DEBUG_ADDRESS_UNION;
```

```csharp
public struct DEBUG_ADDRESS_UNION {
   public ADDRESS_KIND dwKind;
   public IntPtr       unionmember;
}
```

## <a name="members"></a>Membros
`dwKind`\
Um valor da enumeração de [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) , especificando como interpretar a União.

`addr.addrNative`\
[Somente C++] Contém a estrutura de [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) se `dwKind` = ADDRESS_KIND_NATIVE.

`addr.addrThisRel`\
[Somente C++] Contém a estrutura de[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) se `dwKind` = ADDRESS_KIND_UNMANAGED_THIS_RELATIVE.

`addr.addUPhysical`\
[Somente C++] Contém a estrutura de[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) se `dwKind` = ADDRESS_KIND_UNMANAGED_PHYSICAL.

`addr.addrMethod`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) se `dwKind` = ADDRESS_KIND_METHOD.

`addr.addrField`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) se `dwKind` = ADDRESS_KIND_FIELD.

`addr.addrLocal`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) se `dwKind` = ADDRESS_KIND_LOCAL.

`addr.addrParam`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) se `dwKind` = ADDRESS_KIND_PARAM.

`addr.addrArrayElem`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) se `dwKind` = ADDRESS_KIND_ARRAYELEM.

`addr.addrRetVal`\
[Somente C++] Contém a estrutura de[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) se `dwKind` = ADDRESS_KIND_RETVAL.

`addr.unused`\
[Somente C++] preenchimento.

`addr`\
[Somente C++] O nome da União.

`unionmember`\
[Somente C#] Esse valor precisa ser empacotado para o tipo de estrutura apropriado com base em `dwKind` . Consulte comentários para a associação entre `dwKind` e interpretação da União.

## <a name="remarks"></a>Comentários
Essa estrutura faz parte da estrutura de [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) e representa um dos vários tipos diferentes de endereços (a `DEBUG_ADDRESS` estrutura é preenchida por uma chamada para o método [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) ).

 [Somente C#] A tabela a seguir mostra como interpretar o `unionmember` membro para cada tipo de endereço. O exemplo mostra como isso é feito para um tipo de endereço.

|`dwKind`|`unionmember` interpretado como|
|--------------|----------------------------------|
|`ADDRESS_KIND_NATIVE`|[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)|
|`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`|[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)|
|`ADDRESS_KIND_UNMANAGED_PHYSICAL`|[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)|
|`ADDRESS_KIND_METHOD`|[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)|
|`ADDRESS_KIND_FIELD`|[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)|
|`ADDRESS_KIND_LOCAL`|[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)|
|`ADDRESS_KIND_PARAM`|[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)|
|`ADDRESS_KIND_ARRAYELEM`|[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)|
|`ADDRESS_KIND_RETVAL`|[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)|

## <a name="example"></a>Exemplo
Este exemplo mostra como interpretar um tipo de endereço ( `METADATA_ADDRESS_ARRAYELEM` ) da `DEBUG_ADDRESS_UNION` estrutura em C#. Os elementos restantes podem ser interpretados exatamente da mesma maneira.

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(DEBUG_ADDRESS_UNION dau)
        {
            if (dau.dwKind == (uint)enum_ADDRESS_KIND.ADDRESS_KIND_METADATA_ARRAYELEM)
            {
                 METADATA_ADDRESS_ARRAYELEM arrayElem =
                     (METADATA_ADDRESS_ARRAYELEM)Marshal.PtrToStructure(dau.unionmember,
                                 typeof(METADATA_ADDRESS_ARRAYELEM));
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
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
