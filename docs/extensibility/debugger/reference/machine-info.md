---
title: MACHINE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6cbb1020892d496fd5634649484defe26dbd73b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865858"
---
# <a name="machineinfo"></a>MACHINE_INFO
Descreve um determinado computador.

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
 `Fields` Uma combinação de sinalizadores do [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) enumeração que especificam quais campos da estrutura são inicializados.

 `bstrName` O nome do computador. Equivalente a chamar [GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md).

 `Flags` Uma combinação de sinalizadores do [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md) enumeração que descreve os atributos de máquina.

## <a name="remarks"></a>Comentários
 Essa estrutura é retornada por uma chamada para o [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md) método.

## <a name="requirements"></a>Requisitos
 Header: msdbg.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)