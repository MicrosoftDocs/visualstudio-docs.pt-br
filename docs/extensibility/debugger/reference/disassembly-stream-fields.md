---
description: Especifica quais informações recuperar sobre um campo de desmontagem.
title: DISASSEMBLY_STREAM_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8bb45f492a58bd079a1b73212fc9473041d10589
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170465"
---
# <a name="disassembly_stream_fields"></a>DISASSEMBLY_STREAM_FIELDS
Especifica quais informações recuperar sobre um campo de desmontagem.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
typedef DWORD DISASSEMBLY_STREAM_FIELDS;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
```

## <a name="fields"></a>Campos
`DSF_ADDRESS`\
Inicializar/usar o `bstrAddress` campo.

`DSF_ADDRESSOFFSET`\
Inicializar/usar o `bstrAddressOffset` campo.

`DSF_CODEBYTES`\
Inicializar/usar o `bstrCodeBytes` campo.

`DSF_OPCODE`\
Inicializar/usar o `bstrOpCode` campo.

`DSF_OPERANDS`\
Inicializar/usar o `bstrOperands` campo.

`DSF_SYMBOL`\
Inicializar/usar o `bstrSymbol` campo.

`DSF_CODELOCATIONID`\
Inicializar/usar o `uCodeLocationId` campo.

`DSF_POSITION`\
Inicializar/usar os `posBeg` `posEnd` campos e.

`DSF_DOCUMENTURL`\
Inicializar/usar o `bstrDocumentUrl` campo.

`DSF_BYTEOFFSET`\
Inicializar/usar o `dwByteOffset` campo.

`DSF_FLAGS`\
Inicializar/usar o `dwFlags` campo ([DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)).

`DSF_OPERANDS_SYMBOLS`\
Inclua nomes de símbolo no `bstrOperands` campo.

`DSF_ALL`\
Especifica todos os campos para o fluxo de desmontagem.

## <a name="remarks"></a>Comentários
Passado como um parâmetro para o método [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) para indicar quais campos da estrutura [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) devem ser inicializados.

Usado para o `dwFields` membro da `DisassemblyData` estrutura para indicar quais campos são usados e válidos quando a estrutura é retornada.

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [Ler](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
