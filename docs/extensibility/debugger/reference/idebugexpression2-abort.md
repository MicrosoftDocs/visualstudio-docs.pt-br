---
description: Esse método cancela a avaliação de expressão assíncrona como iniciada por uma chamada para o método EvaluateAsync).
title: 'IDebugExpression2:: Abort | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::Abort
helpviewer_keywords:
- IDebugExpression2::Abort
ms.assetid: 4fcb712e-1bdb-4b75-a440-35cc79ee147e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d6c355d2c4ee3cf63551f54b050b0ea42f4fdddc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092443"
---
# <a name="idebugexpression2abort"></a>IDebugExpression2::Abort
Esse método cancela a avaliação de expressão assíncrona como iniciada por uma chamada para o método [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Abort(
   void
);
```

```csharp
int Abort();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando a avaliação de expressão assíncrona é cancelada, não envia um evento [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) para o retorno de chamada de evento passado para os métodos [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) ou [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) .

## <a name="see-also"></a>Confira também
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
