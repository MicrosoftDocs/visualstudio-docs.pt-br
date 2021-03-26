---
description: Essa estrutura fornece informações sobre os processos em execução em um computador.
title: PROVIDER_PROCESS_DATA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_PROCESS_DATA
helpviewer_keywords:
- PROVIDER_PROCESS_DATA structure
ms.assetid: ec2362ed-4a0c-4a09-9d66-8ff04e4f41ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6c48c87f92fde487b9a008c5db45f75eb026f83
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079508"
---
# <a name="provider_process_data"></a>PROVIDER_PROCESS_DATA
Essa estrutura fornece informações sobre os processos em execução em um computador.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagPROVIDER_PROCESS_DATA {
   PROVIDER_FIELDS    Fields;
   PROGRAM_NODE_ARRAY ProgramNodes;
   BOOL               fIsDebuggerPresent;
} PROVIDER_PROCESS_DATA;
```

```csharp
public struct PROVIDER_PROCESS_DATA {
   public uint               Fields;
   public PROGRAM_NODE_ARRAY ProgramNodes;
   public int                fIsDebuggerPresent;
}
```

## <a name="members"></a>Membros
 `Fields`\
 Uma combinação de sinalizadores da enumeração [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md) , indicando quais campos estão preenchidos.

 `ProgramNodes`\
 Uma estrutura de [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) que contém uma matriz de nós de programa.

 `fIsDebuggerPresent`\
 Diferente de zero ( `TRUE` ) se o [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] depurador estiver em execução, zero ( `FALSE` ) se não for.

## <a name="remarks"></a>Comentários
 Essa estrutura é passada para o método [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) em que está preenchida.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)
- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
