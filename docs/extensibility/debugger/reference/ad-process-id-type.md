---
description: Especifica como interpretar uma ID de processo na estrutura de AD_PROCESS_ID.
title: AD_PROCESS_ID_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ae50fc827debd540faa99c33e10ddd217fc691f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094556"
---
# <a name="ad_process_id_type"></a>AD_PROCESS_ID_TYPE
Especifica como interpretar uma ID de processo na estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) .

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
typedef DWORD AD_PROCESS_ID_TYPE;
```

```csharp
public enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
```

## <a name="fields"></a>Campos
`AD_PROCESS_ID_SYSTEM`\
ID do processo é um identificador do sistema. Use o `ProcessId.dwProcessId` campo da estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) .

`AD_PROCESS_ID_GUID`\
A ID do processo é um GUID. Use o `ProcessId.guidProcessId` campo da `AD_PROCESS_ID` estrutura.

## <a name="remarks"></a>Comentários
Usado para o `ProcessIdType` membro da estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) para identificar o tipo de ID de processo que está contido na estrutura. Determina como interpretar a `ProcessId` União na estrutura.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
