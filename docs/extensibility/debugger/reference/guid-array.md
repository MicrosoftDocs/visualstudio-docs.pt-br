---
title: GUID_ARRAY | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eed39ee4446e66e1e7b1700d97ad680eb62c2523
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56704963"
---
# <a name="guidarray"></a>GUID_ARRAY
Descreve uma matriz de identificadores exclusivos para mecanismos de depuração disponíveis.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagGUID_ARRAY
{
    DWORD dwCount;
    GUID *Members;
} GUID_ARRAY;
```

```csharp
public struct GUID_ARRAY
{
    public uint dwCount;
    public Guid Members;
}
```

## <a name="terms"></a>Termos
dwCount número de identificadores exclusivos na matriz.

Matriz de membros que contém identificadores exclusivos.

## <a name="remarks"></a>Comentários
Essa estrutura é retornada pelo [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md) método.

## <a name="requirements"></a>Requisitos
Cabeçalho: Msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)
