---
description: Especifica a quantidade de estado do programa (como threads em execução, quadros de pilha e endereço de instrução atual) a ser despejada.
title: DUMPTYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DUMPTYPE
helpviewer_keywords:
- DUMPTYPE enumeration
ms.assetid: ea8160db-8732-4056-a1d7-892ef72da71e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc27474b0012e60cccadda44665dc368178a02da
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095960"
---
# <a name="dumptype"></a>DUMPTYPE
Especifica a quantidade de estado do programa (como threads em execução, quadros de pilha e endereço de instrução atual) a ser despejada.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
typedef DWORD DUMPTYPE;
```

```csharp
public enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
```

## <a name="fields"></a>Campos
`DUMP_MINIDUMP`\
Especifica um pequeno despejo compacto.

`DUMP_FULLDUMP`\
Especifica um despejo grande e completo.

## <a name="remarks"></a>Comentários
Passado como um argumento para o método [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)
