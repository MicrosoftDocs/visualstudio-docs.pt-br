---
description: Usado para determinar se um programa pode parar a execução depois de atingir um ponto específico na execução.
title: CANSTOP_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CANSTOP_REASON
helpviewer_keywords:
- CANSTOP_REASON enumeration
ms.assetid: 6da944eb-36cd-4a8c-8d71-544c775cfcc1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a22a0534a464e9899e666550b31ab24503c05d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096519"
---
# <a name="canstop_reason"></a>CANSTOP_REASON
Usado para determinar se um programa pode parar a execução depois de atingir um ponto específico na execução.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
typedef DWORD CANSTOP_REASON;
```

```csharp
public enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
```

## <a name="fields"></a>Campos
`CANSTOP_ENTRYPOINT`\
Especifica o ponto de entrada do programa especificado.

`CANSTOP_STEPIN`\
Especifica a depuração em uma função.

## <a name="remarks"></a>Comentários
Passado como um argumento para o método [getmotivo](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) para confirmar com o SDM (Gerenciador de depuração de sessão) se não houver problema para parar depois de atingir o ponto de entrada do programa ou após a depuração em uma função ou método.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
