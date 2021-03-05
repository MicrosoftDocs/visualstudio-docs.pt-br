---
description: Especifica os sinalizadores para desmontagem.
title: DISASSEMBLY_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3aeaf00e7073cd1146dcc5856684ed7209e7d800
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170478"
---
# <a name="disassembly_flags"></a>DISASSEMBLY_FLAGS
Especifica os sinalizadores para desmontagem.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
typedef DWORD DISASSEMBLY_FLAGS;
```

```csharp
public enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
```

## <a name="fields"></a>Campos
`DF_DOCUMENTCHANGE`\
Indica que essa instrução está em um documento diferente do anterior.

`DF_DISABLED`\
Indica que esta instrução não será executada.

`DF_INSTRUCTION_ACTIVE`\
Indica que essa instrução é uma das próximas instruções a serem executadas (pode haver mais de uma).

`DF_DATA`\
Indica que essa instrução é realmente dados (não código).

`DF_HASSOURCE`\
Indica que esta instrução tem fonte. Algumas instruções, como criação de perfil ou código de coleta de lixo, não têm origem correspondente.

`DF_DOCUMENT_CHECKSUM`\
Indica que `bstrDocumentUrl` o campo contém dados de soma de verificação após a URL do documento. Consulte a seção comentários da estrutura [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) para saber como os dados de soma de verificação são armazenados.

## <a name="remarks"></a>Comentários
Usado como o `dwFlags` membro da estrutura [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) .

Esses sinalizadores podem ser combinados com uma operadora de bits `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
