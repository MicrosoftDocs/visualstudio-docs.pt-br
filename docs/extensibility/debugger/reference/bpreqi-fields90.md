---
description: Enumera os valores válidos que especificam as informações a serem recuperadas sobre uma solicitação de ponto de interrupção.
title: BPREQI_FIELDS90 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e977d6e85430dbd9f1931bd4fb62c02f22181d5a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067602"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
Enumera os valores válidos que especificam as informações a serem recuperadas sobre uma solicitação de ponto de interrupção. Essa enumeração estende a enumeração de [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) .

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
typedef DWORD BPREQI_FIELDS90;
```

```csharp
public enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
```

## <a name="fields"></a>Campos
`BPREQI90_BPLOCATION`\
Inicialize ou use o `bpLocation` campo (local do ponto de interrupção) da estrutura [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) ou [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) .

`BPREQI90_LANGUAGE`\
Inicialize ou use o `guidLanguage` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_PROGRAM`\
Inicialize ou use o `pProgram` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_PROGRAMNAME`\
Inicialize ou use o `bstrProgramName` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_THREAD`\
Inicialize ou use o `pThread` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_THREADNAME`\
Inicialize ou use o `bstrThreadName` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_PASSCOUNT`\
Inicialize ou use o `bpPassCount` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_CONDITION`\
Inicialize ou use o `bpCondition` campo (condição de ponto de interrupção) da `BP_REQUEST_INFO` `BP_REQUEST_INFO2` estrutura ou.

`BPREQI90_FLAGS`\
Inicialize ou use o `dwFlags` campo da `BP_REQUEST_INFO` estrutura ou `BP_REQUEST_INFO2` .

`BPREQI90_ALLOLDFIELDS`\
Inicialize ou use todos os campos para a da `BP_REQUEST_INFO` estrutura.

`BPREQI90_VENDOR`\
Inicialize ou use o `guidVendor` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI90_CONSTRAINT`\
Inicialize ou use o `bstrConstraint` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI90_TRACEPOINT`\
Inicialize ou use o `bstrTracepoint` campo de `BP_REQUEST_INFO2` estrutura.

`BPREQI90_MACROTRACEPOINT`\
Inicialize ou use o `bstrMacroTracepoint` campo de `BP_REQUEST_INFO2` estrutura. BPREQI_ALLFIELDS não inclui esse campo.

`BPREQI90_ALLFIELDS`\
Especifica todos os campos para a `BP_REQUEST_INFO2` estrutura.

## <a name="requirements"></a>Requisitos
Cabeçalho: Msdbg90. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
