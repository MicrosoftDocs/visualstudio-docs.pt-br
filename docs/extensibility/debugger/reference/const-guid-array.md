---
title: CONST_GUID_ARRAY | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONST_GUID_ARRAY
helpviewer_keywords:
- CONST_GUID_ARRAY structure
ms.assetid: bd55e7d8-372c-4c3e-9eed-28f6b415a5db
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c0021ef24e0cafec0119263d2c74175f0d38d784
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737627"
---
# <a name="const_guid_array"></a>CONST_GUID_ARRAY
Uma estrutura que contém uma lista de `GUID` s.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagCONST_GUID_ARRAY {
    DWORD       dwCount;
    CONST GUID* Members;
} CONST_GUID_ARRAY;
```

```csharp
public struct CONST_GUID_ARRAY {
    public uint   dwCount;
    public Guid[] Members;
}
```

## <a name="members"></a>Membros
`dwCount`\
Número de `GUID` s na `Members` matriz.

`Members`\
Matriz de `GUID` s.

## <a name="remarks"></a>Comentários
Essa estrutura é passada para o método [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) e é retornada dos métodos [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) e [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md) .

O proprietário de uma instância dessa estrutura é responsável por liberar memória alocada.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
