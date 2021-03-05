---
description: Determina se um processo pode ser encerrado.
title: 'IDebugPortEx2:: CanTerminateProcess | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::CanTerminateProcess
helpviewer_keywords:
- IDebugPortEx2::CanTerminateProcess
ms.assetid: 111f65d8-5a1a-42b3-9de3-dd9bb03a33fd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11a850f844a77c0e137a7a6603ac14b31e7dc326
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169451"
---
# <a name="idebugportex2canterminateprocess"></a>IDebugPortEx2::CanTerminateProcess
Determina se um processo pode ser encerrado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanTerminateProcess( 
   IDebugProcess2* pPortProcess
);
```

```csharp
HRESULT CanTerminateProcess( 
   IDebugProcess2 pPortProcess
);
```

## <a name="parameters"></a>Parâmetros
`pPortProcess`\
no Um objeto [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) que representa o processo a ser encerrado.

## <a name="return-value"></a>Valor Retornado
 Retorna `S_OK` se o processo pode ser encerrado; caso contrário, retorna `S_FALSE` .

## <a name="see-also"></a>Confira também
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
