---
title: Avaliando uma expressão de janela de inspeção | Microsoft Docs
description: Saiba como o Visual Studio chama o mecanismo de depuração para determinar o valor atual de cada expressão em sua lista de observação quando a execução pausa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e72a89a6d3b51a328294d5bfa56e1699ead5498a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097065"
---
# <a name="evaluate-a-watch-window-expression"></a>Avaliar uma expressão de janela de inspeção
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Quando a execução é pausada, o Visual Studio chama o mecanismo de depuração (DE) para determinar o valor atual de cada expressão em sua lista de observação. O DE avalia cada expressão usando um avaliador DE expressão (EE) e o Visual Studio exibe seu valor na janela **Watch** .

 Veja a seguir uma visão geral de como uma expressão de lista de observação é avaliada:

1. O Visual Studio chama o [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) de ' s para obter um contexto de expressão que pode ser usado para avaliar expressões.

2. Para cada expressão na lista de observação, o Visual Studio chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para converter o texto da expressão em uma expressão analisada.

3. `IDebugExpressionContext2::ParseText` chama [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para fazer o trabalho real de analisar o texto e produzir um objeto [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) .

4. `IDebugExpressionContext2::ParseText` Cria um objeto [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) e coloca o `IDebugParsedExpression` objeto nele. Esse `DebugExpression2` objeto I é retornado para o Visual Studio.

5. O Visual Studio chama [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para avaliar a expressão analisada.

6. `IDebugExpression2::EvaluateSync` passa a chamada para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) para fazer a avaliação real e produzir um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que é retornado para o Visual Studio.

7. O Visual Studio chama [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) para obter o valor da expressão que é exibida na lista de observação.

## <a name="parse-then-evaluate"></a>Analisar e avaliar
 Como a análise de uma expressão complexa pode levar muito mais tempo do que avaliá-la, o processo de avaliação de uma expressão é dividido em duas etapas: 1) analisar a expressão e 2) avaliar a expressão analisada. Dessa forma, a avaliação pode ocorrer muitas vezes, mas a expressão precisa ser analisada apenas uma vez. A expressão analisada intermediária é retornada do EE em um objeto [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) que, por sua vez, é encapsulado e RETORNADO do de como um objeto [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) . O `IDebugExpression` objeto adia toda a avaliação para o `IDebugParsedExpression` objeto.

> [!NOTE]
> Não é necessário que um EE obedeça a esse processo de duas etapas, embora o Visual Studio assuma isso; o EE pode analisar e avaliar na mesma etapa quando [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) é chamado (é assim que o exemplo de MyCEE funciona, por exemplo). Se sua linguagem puder formar expressões complexas, talvez você queira separar a etapa de análise da etapa de avaliação. Isso pode aumentar o desempenho no depurador do Visual Studio quando muitas expressões de inspeção estão sendo mostradas.

## <a name="in-this-section"></a>Nesta seção
 [Exemplo de implementação de avaliação de expressão](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md) Usa o exemplo MyCEE para percorrer o processo de avaliação de expressão.

 [Avaliando uma expressão Watch](../../extensibility/debugger/evaluating-a-watch-expression.md) Explica o que acontece após uma análise de expressão bem-sucedida.

## <a name="related-sections"></a>Seções relacionadas
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md) Fornece os argumentos que são passados quando o mecanismo de depuração (DE) chama o avaliador de expressão (EE).

## <a name="see-also"></a>Confira também
 [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
