---
title: Avaliação de expressão no modo de interrupção | Microsoft Docs
description: Saiba mais sobre o processo que ocorre quando o depurador está no modo de interrupção e deve realizar a avaliação da expressão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 932bebecf4eea73cfae579bbea58e024b4388ffb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067862"
---
# <a name="expression-evaluation-in-break-mode"></a>Avaliação de expressão no modo de interrupção
A seção a seguir descreve o processo que ocorre quando o depurador está no modo de interrupção e deve realizar a avaliação da expressão.

## <a name="expression-evaluation-process"></a>Processo de avaliação de expressão
 A seguir estão as etapas básicas envolvidas na avaliação de uma expressão:

1. O SDM (Gerenciador de depuração de sessão) chama [IDebugStackFrame2:: GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter uma interface de contexto de expressão, [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md).

2. Em seguida, o SDM chama [IDebugExpressionContext2::P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) com a cadeia de caracteres a ser analisada.

3. Se ParseText não retornar S_OK, o motivo do erro será retornado.

     ,

     Se ParseText retornar S_OK, o SDM poderá chamar [IDebugExpression2:: EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [IDebugExpression2:: EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter um valor final da expressão analisada.

    - Ao usar `IDebugExpression2::EvaluateSync` o, a interface de retorno de chamada fornecida comunica o processo contínuo da avaliação. O valor final é retornado em uma interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) .

    - Ao usar `IDebugExpression2::EvaluateAsync` o, a interface de retorno de chamada fornecida comunica o processo contínuo da avaliação. Depois que a avaliação for concluída, o EvaluateAsync enviará uma interface [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) por meio do retorno de chamada. Com essa interface de evento, o valor final resulta com [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md).

## <a name="see-also"></a>Confira também
- [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
