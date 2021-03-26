---
description: Especifica quais informações recuperar sobre um objeto de propriedade de depuração.
title: DEBUGPROP_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS enumeration
ms.assetid: 1c7fe777-615e-4929-9ed4-970d9fe0eb81
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84e52867c44fa1387aaf7501a827168651099e9c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096207"
---
# <a name="debugprop_info_flags"></a>DEBUGPROP_INFO_FLAGS
Especifica quais informações recuperar sobre um objeto de propriedade de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
typedef DWORD DEBUGPROP_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
```

## <a name="fields"></a>Campos
`DEBUGPROP_INFO_FULLNAME`\
Inicializar/usar o `bstrFullName` campo.

`DEBUGPROP_INFO_NAME`\
Inicializar/usar o `bstrName` campo.

`DEBUGPROP_INFO_TYPE`\
Inicializar/usar o `bstrType` campo.

`DEBUGPROP_INFO_VALUE`\
Inicializar/usar o `bstrValue` campo.

`DEBUGPROP_INFO_ATTRIB`\
Inicializar/usar o `dwAttrib` campo.

`DEBUGPROP_INFO_PROP`\
Inicializar/usar o `pProperty` campo que contém uma interface [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) .

`DEBUGPROP_INFO_VALUE_AUTOEXPAND`\
Especifica que o campo de valor deve conter o valor expandido automaticamente, se disponível, para esse tipo de objeto.

`DEBUGPROP_INFO_VALUE_NOFUNCEVAL`\
Preterido.

`DEBUGPROP_INFO_VALUE_RAW`\
Não retornar nenhum valor ou membro de beautified (ou seja, não formatar os valores).

`DEBUGPROP_INFO_VALUE_NO_TOSTRING`\
Não retornar nenhum valor especial sintetizado (por exemplo, não chame `ToString()` em um objeto para produzir um Value).

`DEBUGPROP_INFO_NONE`\
Especifica que nenhum sinalizador está definido.

`DEBUGPROP_INFO_STANDARD`\
Inicialize/use os `dwAttrib` `bstrName` campos,, e `bstrType` `bstrValue` .

`DEBUGPROP_INFO_All`\
Indica uma máscara de todos os sinalizadores.

## <a name="remarks"></a>Comentários
Esses valores são passados para os métodos [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md), [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)e [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) para indicar quais campos devem ser inicializados na estrutura de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) .

Esses valores também são usados para o `dwFields` membro da `DEBUG_PROPERTY_INFO` estrutura para indicar quais campos da estrutura são usados e válidos quando a estrutura é retornada.

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
