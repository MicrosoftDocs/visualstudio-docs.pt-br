---
description: Especifica quais informações recuperar sobre um objeto de referência de depuração.
title: DEBUGREF_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 913490588fcf739e9659318cb72a9ca74d6db99d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096220"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
Especifica quais informações recuperar sobre um objeto de referência de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
typedef DWORD DEBUGREF_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
```

## <a name="fields"></a>Campos
`DEBUGREF_INFO_NAME`\
Inicializar/usar o `bstrName` campo na estrutura.

`DEBUGREF_INFO_TYPE`\
Inicializar/usar o `bstrType` campo na estrutura.

`DEBUGREF_INFO_VALUE`\
Inicializar/usar o `bstrValue` campo na estrutura.

`DEBUGREF_INFO_ATTRIB`\
Inicializar/usar o `dwAttrib` campo na estrutura.

`DEBUGREF_INFO_REFTYPE`\
Inicializar/usar o `dwRefType` campo na estrutura.

`DEBUGREF_INFO_REF`\
Inicializar/usar o `pReference` campo na estrutura.

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
O campo valor deve conter o valor expandido automaticamente, se disponível, para esse tipo de objeto.

`DEBUGREF_INFO_NONE`\
Indica que nenhum sinalizador está definido.

`DEBUGREF_INFO_ALL`\
Indica uma máscara dos sinalizadores.

## <a name="remarks"></a>Comentários
Esses sinalizadores são passados para os métodos [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) e [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) para indicar quais campos da estrutura de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) devem ser inicializados.

Usado para o `dwFields` membro da `DEBUG_REFERENCE_INFO` estrutura para indicar quais campos são usados e válidos quando a estrutura é retornada.

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
