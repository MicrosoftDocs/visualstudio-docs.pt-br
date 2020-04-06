---
title: MACHINE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad66992bd07afa2ef563c1b58fab0172e9a6121e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714540"
---
# <a name="machine_info"></a>MACHINE_INFO
Descreve uma máquina em particular.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagMACHINE_INFO { 
   MACHINE_INFO_FIELDS Fields;
   BSTR                bstrName;
   MACHINE_INFO_FLAGS  Flags;
} MACHINE_INFO;
```

```csharp
public struct MACHINE_INFO { 
   public uint   Fields;
   public string bstrName;
   public uint   Flags;
};
```

## <a name="members"></a>Membros
 `Fields`\
 Uma combinação de bandeiras da [enumeração MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) que especificam quais campos da estrutura são inicializados.

 `bstrName`\
 O nome da máquina. Equivalente a chamar [GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md).

 `Flags`\
 Uma combinação de bandeiras da [enumeração MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md) descrevendo os atributos da máquina.

## <a name="remarks"></a>Comentários
 Essa estrutura é devolvida por uma chamada para o método [GetMachineInfo.](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Montagem: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
