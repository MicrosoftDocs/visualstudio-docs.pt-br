---
title: DEBUG_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0502ab10398d37bcafee5316ba7e7566dbab4e01
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346160"
---
# <a name="debugreason"></a>DEBUG_REASON
Especifica por que o processo foi iniciado para depuração.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
typedef DWORD DEBUG_REASON;
```

```csharp
public enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
```

## <a name="fields"></a>Campos
`DEBUG_REASON_ERROR`\
Ocorreu um erro não específico (Isso é usado como uma condição padrão quando nenhuma das outras questões de ajuste).

`DEBUG_REASON_USER_LAUNCHED`\
O processo foi iniciado mediante solicitação do usuário.

`DEBUG_REASON_USER_ATTACHED`\
O processo de execução já foi anexado pelo usuário.

`DEBUG_REASON_AUTO_ATTACHED`\
O processo foi anexado automaticamente a quando ele foi iniciado.

`DEBUG_REASON_CAUSALITY`\
O processo foi iniciado devido a um *Just-In-Time* eventos de depuração (JIT).

## <a name="remarks"></a>Comentários
Retornado do [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md) método.

## <a name="requirements"></a>Requisitos
Header: msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
