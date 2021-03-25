---
title: Exemplo de implementação de avaliação de expressão | Microsoft Docs
description: Saiba como o Visual Studio chama ParseText para produzir um objeto IDebugExpression2 para uma expressão de inspeção do Windows.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 60d01917bb3a21f6d8ea2644fbeef2b22064cc00
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070447"
---
# <a name="sample-implementation-of-expression-evaluation"></a>Exemplo de implementação de avaliação de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Para uma expressão de janela de **inspeção** , o Visual Studio chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para produzir um objeto [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) . `IDebugExpressionContext2::ParseText` Cria uma instância de um avaliador de expressão (EE) e chama [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para obter um objeto [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) .

 O `IDebugExpressionEvaluator::Parse` executa as seguintes tarefas:

1. [Somente C++] Analisa a expressão para procurar erros.

2. Cria uma instância de uma classe (chamada `CParsedExpression` neste exemplo) que executa a `IDebugParsedExpression` interface e armazena na classe a expressão a ser analisada.

3. Retorna a `IDebugParsedExpression` interface do `CParsedExpression` objeto.

> [!NOTE]
> Nos exemplos a seguir e no exemplo MyCEE, o avaliador de expressão não separa a análise da avaliação.

## <a name="managed-code"></a>Código gerenciado
 O código a seguir mostra uma implementação do `IDebugExpressionEvaluator::Parse` em código gerenciado. Esta versão do método adia a análise para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) , pois o código para análise também é avaliado ao mesmo tempo (consulte [avaliar uma expressão Watch](../../extensibility/debugger/evaluating-a-watch-expression.md)).

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT Parse(
                string                 expression,
                uint                   parseFlags,
                uint                   radix,
            out string                 errorMessage,
            out uint                   errorPosition,
            out IDebugParsedExpression parsedExpression)
        {
            errorMessage = "";
            errorPosition = 0;

            parsedExpression =
                new CParsedExpression(parseFlags, radix, expression);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>Código não gerenciado
O código a seguir é uma implementação do `IDebugExpressionEvaluator::Parse` em código não gerenciado. Esse método chama uma função auxiliar, `Parse` , para analisar a expressão e verificar se há erros, mas esse método ignora o valor resultante. A avaliação formal é adiada para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) em que a expressão é analisada enquanto é avaliada (consulte [avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)).

```cpp
STDMETHODIMP CExpressionEvaluator::Parse(
        in    LPCOLESTR                 pszExpression,
        in    PARSEFLAGS                flags,
        in    UINT                      radix,
        out   BSTR                     *pbstrErrorMessages,
        inout UINT                     *perrorCount,
        out   IDebugParsedExpression  **ppparsedExpression
    )
{
    if (pbstrErrorMessages == NULL)
        return E_INVALIDARG;
    else
        *pbstrErrormessages = 0;

    if (pparsedExpression == NULL)
        return E_INVALIDARG;
    else
        *pparsedExpression = 0;

    if (perrorCount == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    // Look for errors in the expression but ignore results
    hr = ::Parse( pszExpression, pbstrErrorMessages );
    if (hr != S_OK)
        return hr;

    CParsedExpression* pparsedExpr = new CParsedExpression( radix, flags, pszExpression );
    if (!pparsedExpr)
        return E_OUTOFMEMORY;

    hr = pparsedExpr->QueryInterface( IID_IDebugParsedExpression,
                                      reinterpret_cast<void**>(ppparsedExpression) );
    pparsedExpr->Release();

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [Avaliar uma expressão de janela Inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [Avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)
