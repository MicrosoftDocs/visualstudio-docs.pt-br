---
description: Especifica o estado do thread.
title: THREADSTATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADSTATE
helpviewer_keywords:
- THREADSTATE enumeration
ms.assetid: 62efdd7c-25b1-4fd3-9d06-ac1830a418a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 513e90e649d71a4fb7d5bc220eb9752925151d9f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070811"
---
# <a name="threadstate"></a>THREADSTATE
Especifica o estado do thread.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
typedef DWORD THREADSTATE;
```

```csharp
public enum enum_THREADSTATE { 
   THREADSTATE_RUNNING = 0x0001,
   THREADSTATE_STOPPED = 0x0002,
   THREADSTATE_FRESH   = 0x0003,
   THREADSTATE_DEAD    = 0x0004,
   THREADSTATE_FROZEN  = 0x0005
};
```

## <a name="fields"></a>Campos
 `THREADSTATE_RUNNING`\
 Indica que o thread está em execução.

 `THREADSTATE_STOPPED`\
 Indica que o thread foi interrompido devido a um ponto de interrupção.

 `THREADSTATE_FRESH`\
 Indica que o thread foi criado, mas que ainda não está executando o código.

 `THREADSTATE_DEAD`\
 Indica que o thread está inativo.

 `THREADSTATE_FROZEN`\
 Indica que o thread está congelado (nenhuma execução pode ser executada).

## <a name="remarks"></a>Comentários
 Usado para o `dwThreadState` campo da estrutura [threadproperties](../../../extensibility/debugger/reference/threadproperties.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
