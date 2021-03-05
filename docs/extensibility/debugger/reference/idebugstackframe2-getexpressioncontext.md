---
description: Obtém um contexto de avaliação para avaliação de expressão dentro do contexto atual de um quadro de pilha e thread.
title: 'IDebugStackFrame2:: GetExpressionContext | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetExpressionContext
helpviewer_keywords:
- IDebugStackFrame2::GetExpressionContext
ms.assetid: a2604e6a-502d-473b-868f-b11ac64c7a35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4780b979102ee2ada499e2cd2e0f8ca728cadd91
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145931"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
Obtém um contexto de avaliação para avaliação de expressão dentro do contexto atual de um quadro de pilha e thread.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetExpressionContext ( 
   IDebugExpressionContext2** ppExprCxt
);
```

```csharp
int GetExpressionContext ( 
   out IDebugExpressionContext2 ppExprCxt
);
```

## <a name="parameters"></a>Parâmetros
`ppExprCxt`\
fora Retorna um objeto [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) que representa um contexto para avaliação de expressão.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Em geral, um contexto de avaliação de expressão pode ser considerado como um escopo para executar a avaliação da expressão. Chame o método [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para analisar uma expressão e, em seguida, chame os métodos [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) resultantes para avaliar a expressão analisada.

## <a name="see-also"></a>Confira também
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
