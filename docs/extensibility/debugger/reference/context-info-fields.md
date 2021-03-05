---
description: Especifica quais informações recuperar sobre um contexto de memória.
title: CONTEXT_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 401195d5b03f87ba1ea5c66811570a720e53bdae
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170764"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
Especifica quais informações recuperar sobre um contexto de memória.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
typedef DWORD CONTEXT_INFO_FIELDS;
```

```csharp
public enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
```

## <a name="fields"></a>Campos
`CIF_MODULEURL`\
Inicializar/usar o `bstrModuleUrl` campo da estrutura de [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) .

`CIF_FUNCTION`\
Inicializar/usar o `bstrFunction` campo da `CONTEXT_INFO` estrutura.

`CIF_FUNCTIONOFFSET`\
Inicializar/usar o `posFunctionOffset` campo da `CONTEXT_INFO` estrutura.

`CIF_ADDRESS`\
Inicializar/usar o `bstrAddress` campo da `CONTEXT_INFO` estrutura.

`CIF_ADDRESSOFFSET`\
Inicializar/usar o `bstrAddressOffset` campo da `CONTEXT_INFO` estrutura.

`CIF_ALLFIELDS`\
Inicializar/usar todos os campos da `CONTEXT_INFO` estrutura.

## <a name="remarks"></a>Comentários
Esses valores passam um parâmetro para o método [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) para indicar quais campos da estrutura de [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) devem ser inicializados.

Esses sinalizadores também são usados para indicar quais campos da `CONTEXT_INFO` estrutura são usados e válidos quando a estrutura é retornada.

Esses valores podem ser combinados com um OR bit a bit.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
