---
description: Especifica os tipos de endereços.
title: ADDRESS_KIND | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ADDRESS_KIND
helpviewer_keywords:
- ADDRESS_KIND enumeration
ms.assetid: 3a12fbec-7088-4cf9-8f6f-ad8ddec6009a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 12a47edf2b9eca9cd99a5b11531f78e080572d54
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144644"
---
# <a name="address_kind"></a>ADDRESS_KIND
Especifica os tipos de endereços.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
typedef DWORD ADDRESS_KIND;
```

```csharp
public enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
```

## <a name="fields"></a>Campos
`ADDRESS_KIND_NATIVE`\
Um endereço nativo, representado pela estrutura de [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) .

`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`\
Um endereço não gerenciado relativo a um `this` ponteiro ( `Me` no Visual Basic) e representado pela estrutura de [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) .

`ADDRESS_KIND_UNMANAGED_PHYSICAL`\
Um endereço físico não gerenciado, representado pela estrutura de [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) .

`ADDRESS_KIND_METHOD`\
Um método de uma classe, representado pela estrutura de [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) .

`ADDRESS_KIND_FIELD`\
Um campo de uma classe, representado pela estrutura de [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) .

`ADDRESS_KIND_LOCAL`\
O endereço é para uma variável local e é representado pela estrutura de [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) .

`ADDRESS_KIND_PARAM`\
Um método ou parâmetro de função, representado pela estrutura de [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) .

`ADDRESS_KIND_ARRAYELEM`\
Um elemento de matriz, representado pela estrutura de [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) .

`ADDRESS_KIND_RETVAL`\
Um valor de retorno, representado pela estrutura de [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) .

## <a name="remarks"></a>Comentários
O método [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) retorna a estrutura de [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) que contém uma União de estruturas possíveis, a estrutura de [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) . O `dwKind` campo da `DEBUG_ADDRESS_UNION` estrutura contém o `ADDRESS_KIND` valor e descreve como interpretar o campo Union.

## <a name="requirements"></a>Requisitos
Cabeçalho: sh. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
