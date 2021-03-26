---
description: Contém informações sobre uma propriedade de depuração.
title: DEBUG_PROPERTY_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_PROPERTY_INFO
helpviewer_keywords:
- DEBUG_PROPERTY_INFO structure
ms.assetid: 5a085d18-62c6-4740-b9e9-3f5db6bfdf7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13e780dd5d6825515673547aae8f3dc16edd885c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096285"
---
# <a name="debug_property_info"></a>DEBUG_PROPERTY_INFO
Contém informações sobre uma propriedade de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagDEBUG_PROPERTY_INFO {
    DEBUGPROP_INFO_FLAGS dwValidFields;
    BSTR                 bstrFullName;
    BSTR                 bstrName;
    BSTR                 bstrType;
    BSTR                 bstrValue;
    IDebugProperty2*     pProperty;
    DBG_ATTRIB_FLAGS     dwAttrib;
} DEBUG_PROPERTY_INFO;
```

```csharp
public struct DEBUG_PROPERTY_INFO {
    public uint            dwValidFields;
    public string          bstrFullName;
    public string          bstrName;
    public string          bstrType;
    public string          bstrValue;
    public IDebugProperty2 pProperty;
    public ulong           dwAttrib;
};
```

## <a name="members"></a>Membros
`dwValidFields`\
Uma combinação de sinalizadores da enumeração [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) que especifica quais campos são preenchidos.

`bstrFullName`\
O nome completo da propriedade.

`bstrName`\
O nome da propriedade dentro de um contexto.

`bstrType`\
O tipo de propriedade como uma cadeia de caracteres formatada.

`bstrValue`\
O valor da propriedade como uma cadeia de caracteres formatada.

`pProperty`\
O objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) descrito por essa estrutura.

`dwAttrib`\
Uma combinação de sinalizadores da enumeração de [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) que descreve os atributos dessa propriedade.

## <a name="remarks"></a>Comentários
Uma propriedade é um objeto de uma natureza hierárquica que tem um nome, tipo e valor. Por exemplo, uma propriedade pode descrever variáveis locais, parâmetros, variáveis de inspeção e expressões e registros.

Essa estrutura é passada para o método [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) em que está preenchida. Essa estrutura também é retornada como parte de uma lista dessa estrutura da interface [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) que, por sua vez, é retornada de uma chamada para os métodos [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) e [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
