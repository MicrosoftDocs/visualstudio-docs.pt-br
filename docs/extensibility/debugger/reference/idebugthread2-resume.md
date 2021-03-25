---
description: Retoma a execução de um thread.
title: 'IDebugThread2:: resume | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93552bac60d16a21212bfa89816481cf7099d399
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053016"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
Retoma a execução de um thread.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>Parâmetros
`pdwSuspendCount`\
fora Retorna a contagem de suspensão após a operação de retomada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Cada chamada para esse método diminui a contagem de suspensões até chegar a 0 em que momento, a execução é realmente retomada. Essa contagem de suspensão é exibida na janela de depuração de **threads** .

 Para cada chamada para esse método, deve haver uma chamada anterior para o método [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md) . A contagem de suspensão determina quantas vezes o `IDebugThread2::Suspend` método foi chamado até o momento.

## <a name="see-also"></a>Confira também
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
