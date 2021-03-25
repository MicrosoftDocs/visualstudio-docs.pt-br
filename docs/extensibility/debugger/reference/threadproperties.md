---
description: Descreve as propriedades de um thread.
title: THREADPROPERTIES | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0707cb5da4c63ffd686f22fa691c103c954478c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070850"
---
# <a name="threadproperties"></a>THREADPROPERTIES
Descreve as propriedades de um thread.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagTHREADPROPERTIES { 
   THREADPROPERTY_FIELDS dwFields;
   DWORD                 dwThreadId;
   DWORD                 dwSuspendCount;
   DWORD                 dwThreadState;
   BSTR                  bstrPriority;
   BSTR                  bstrName;
   BSTR                  bstrLocation;
} THREADPROPERTIES;
```

```csharp
public struct THREADPROPERTIES { 
   public uint   dwFields;
   public uint   dwThreadId;
   public uint   dwSuspendCount;
   public uint   dwThreadState;
   public string bstrPriority;
   public string bstrName;
   public string bstrLocation;
};
```

## <a name="members"></a>Membros
 `dwFields`\
 Uma combinação de sinalizadores da enumeração [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md) , que descreve quais campos nessa estrutura são válidos.

 `dwThreadId`\
 A ID do thread.

 `dwSuspendCount`\
 A contagem de suspensões de thread.

 `dwThreadState`\
 Um valor da enumeração [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md) que indica o estado do thread operacional.

 `bstrPriority`\
 Uma cadeia de caracteres que especifica a prioridade do thread; por exemplo, "acima do normal", "normal" ou "tempo crítico".

 `bstName`\
 O nome do thread.

 `bstrLocation`\
 O local do thread (geralmente o quadro de pilha superior), normalmente expresso como o nome do método em que a execução está interrompida no momento.

## <a name="remarks"></a>Comentários
 Essa estrutura é preenchida por uma chamada para o método [Getthreadproperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) . As informações retornadas normalmente são usadas para preencher a janela **threads** .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
