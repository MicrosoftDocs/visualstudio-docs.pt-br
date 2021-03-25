---
description: Contém informações sobre um processo.
title: PROCESS_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b6fe223d67b876dca1604b2617a33a888ec8180c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079635"
---
# <a name="process_info"></a>PROCESS_INFO
Contém informações sobre um processo.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagPROCESS_INFO { 
   PROCESS_INFO_FIELDS Fields;
   BSTR                bstrFileName;
   BSTR                bstrBaseName;
   BSTR                bstrTitle;
   AD_PROCESS_ID       ProcessId;
   DWORD               dwSessionId;
   BSTR                bstrAttachedSessionName;
   FILETIME            CreationTime;
   PROCESS_INFO_FLAGS  Flags;
} PROCESS_INFO;
```

```csharp
public struct PROCESS_INFO { 
   public uint          Fields;
   public string        bstrFileName;
   public string        bstrBaseName;
   public string        bstrTitle;
   public AD_PROCESS_ID ProcessId;
   public uint          dwSessionId;
   public string        bstrAttachedSessionName;
   public FILETIME      CreationTime;
   public uint          Flags;
};
```

## <a name="members"></a>Membros
 `Fields`\
 Uma combinação de sinalizadores da enumeração de [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md) que especifica quais campos são preenchidos.

 `bstrFileName`\
 O nome do caminho completo do processo. Equivalente a chamar o método [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) com o parâmetro `GN_FILENAME` .

 `bstrBaseName`\
 O nome do arquivo e a extensão do processo. Equivalente a chamar o `IDebugProcess2::Getname` método com o parâmetro `GN_BASENAME` .

 `bstrTitle`\
 O título do processo, se houver. Equivalente a chamar o `IDebugProcess2::Getname` método com o parâmetro `GN_TITLE` .

 `ProcessId`\
 A estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) que identifica o processo. Equivalente a chamar o método [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md) .

 `dwSessionId`\
 O identificador da sessão de depuração em que esse processo está sendo executado.

 `bstrAttachedSessionName`\
 O nome da sessão anexada. Equivalente a chamar o método [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md) .

 `CreationTime`\
 A hora em que o processo foi criado.

 `Flags`\
 Uma combinação de sinalizadores da enumeração [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md) que especificam as propriedades do processo.

## <a name="remarks"></a>Comentários
 Essa estrutura é passada para o método [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) onde está preenchida.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)
- [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
