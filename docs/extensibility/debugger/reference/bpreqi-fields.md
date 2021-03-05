---
description: Especifica as informações a serem recuperadas sobre uma solicitação de ponto de interrupção.
title: BPREQI_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f7ee5d8dbf48ad8d1b07512727b1b91635ab990
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162453"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
Especifica as informações a serem recuperadas sobre uma solicitação de ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
typedef DWORD BPREQI_FIELDS;
```

```csharp
public enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
```

## <a name="fields"></a>Campos
`BPREQI_BPLOCATION`\
Inicializar/usar o `bpLocation` campo (local do ponto de interrupção) da estrutura [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) ou [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) .

`BPREQI_LANGUAGE`\
Inicializar/usar o `guidLanguage` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_PROGRAM`\
Inicializar/usar o `pProgram` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_PROGRAMNAME`\
Inicializar/usar o `bstrProgramName` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_THREAD`\
Inicializar/usar o `pThread` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_THREADNAME`\
Inicializar/usar o `bstrThreadName` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_PASSCOUNT`\
Inicializar/usar o `bpPassCount` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_CONDITION`\
Inicializar/usar o `bpCondition` campo (condição de ponto de interrupção) da `BP_REQUEST_INFO` `BP_REQUEST_INFO2` estrutura ou.

`BPREQI_FLAGS`\
Inicializar/usar o `dwFlags` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI_ALLOLDFIELDS`\
Inicializar/usar todos os campos para a da `BP_REQUEST_INFO` estrutura.

`BPREQI_VENDOR`\
Inicializar/usar o `guidVendor` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI_CONSTRAINT`\
Inicializar/usar o `bstrConstraint` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI_TRACEPOINT`\
Inicializar/usar o `bstrTracepoint` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI_ALLFIELDS`\
Especifica todos os campos para a `BP_REQUEST_INFO2` estrutura.

## <a name="remarks"></a>Comentários
Passado como um argumento para os métodos [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) e [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) para especificar quais campos das estruturas [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) e [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) devem ser inicializados.

Esses sinalizadores também são usados para indicar quais campos das `BP_REQUEST_INFO` estruturas e `BP_REQUEST_INFO2` são usados e válidos quando cada estrutura é retornada.

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
