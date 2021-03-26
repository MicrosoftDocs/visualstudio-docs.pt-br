---
description: Esse método avalia a expressão de forma assíncrona.
title: 'IDebugExpression2:: EvaluateAsync | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bea7a5a05dc5277e693d033452f0b4e7342ea946
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092417"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
Esse método avalia a expressão de forma assíncrona.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EvaluateAsync (
    EVALFLAGS             dwFlags,
    IDebugEventCallback2* pExprCallback
);
```

```csharp
int EvaluateAsync(
    enum_EVALFLAGS       dwFlags,
    IDebugEventCallback2 pExprCallback
);
```

## <a name="parameters"></a>Parâmetros
`dwFlags`\
no Uma combinação de sinalizadores da enumeração [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) que controlam a avaliação da expressão.

`pExprCallback`\
no Esse parâmetro é sempre um valor nulo.

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Um código de erro típico é:

|Erro|Descrição|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|Outra expressão está sendo avaliada no momento e não há suporte para a avaliação de expressão simultânea.|

## <a name="remarks"></a>Comentários
Esse método deve retornar imediatamente depois de ter iniciado a avaliação da expressão. Quando a expressão é avaliada com êxito, um [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) deve ser enviado para o retorno de chamada do evento [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) , conforme fornecido por meio de [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) ou [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md).

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CExpression` objeto simples que implementa a interface [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) .

```cpp
HRESULT CExpression::EvaluateAsync(EVALFLAGS dwFlags,
                                   IDebugEventCallback2* pExprCallback)
{
    // Set the aborted state to FALSE
    // in case the user tries to redo the evaluation after aborting.
    m_bAborted = FALSE;
    // Post the WM_EVAL_EXPR message in the message queue of the current thread.
    // This starts the expression evaluation on a background thread.
    PostThreadMessage(GetCurrentThreadId(), WM_EVAL_EXPR, 0, (LPARAM) this);
    return S_OK;
}
```

## <a name="see-also"></a>Confira também
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
