---
title: Implementação de exemplo de avaliação de expressão | Microsoft Docs
description: Saiba como Visual Studio chama ParseText para produzir um objeto IDebugExpression2 para uma expressão de Janela de Relógio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: sample
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
ms.openlocfilehash: de0e052fd42f1603889f7521a1e45e50b0f36eea
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902300"
---
# <a name="sample-implementation-of-expression-evaluation"></a>Implementação de exemplo de avaliação de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte Avaliadores de expressão [CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e Exemplo de avaliador [de expressão gerenciada.](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

 Para uma **expressão de** janela De Visual Studio, chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para produzir um [objeto IDebugExpression2.](../../extensibility/debugger/reference/idebugexpression2.md) `IDebugExpressionContext2::ParseText`instalita um avaliador de expressão (EE) e chama [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para obter um [objeto IDebugParsedExpression.](../../extensibility/debugger/reference/idebugparsedexpression.md)

 O `IDebugExpressionEvaluator::Parse` executa as seguintes tarefas:

1. [Somente C++ ] Analisar a expressão para procurar erros.

2. Instalita uma classe (chamada neste exemplo) que executa a interface e armazena na classe a expressão a `CParsedExpression` `IDebugParsedExpression` ser analisado.

3. Retorna a `IDebugParsedExpression` interface do `CParsedExpression` objeto .

> [!NOTE]
> Nos exemplos a seguir e no exemplo myCEE, o avaliador de expressão não separa a análise da avaliação.

## <a name="managed-code"></a>Código gerenciado
 O código a seguir mostra uma implementação de `IDebugExpressionEvaluator::Parse` no código gerenciado. Esta versão do método adia a análise para [EvaluateSync,](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) pois o código para análise também é avaliada ao mesmo tempo (consulte Avaliar uma expressão [de relógio](../../extensibility/debugger/evaluating-a-watch-expression.md)).

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

## <a name="unmanaged-code"></a>Código nãomanagedo
O código a seguir é uma implementação `IDebugExpressionEvaluator::Parse` de em código nãomanagedo. Esse método chama uma função auxiliar, , para analisar a expressão e verificar se há erros, mas esse método ignora o `Parse` valor resultante. A avaliação formal é adiada para [EvaluateSync,](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) em que a expressão é analisado enquanto ela é avaliada (consulte [Avaliar uma expressão de relógio](../../extensibility/debugger/evaluating-a-watch-expression.md)).

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
- [Avaliar uma expressão janela Inspeção dados](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [Avaliar uma expressão watch](../../extensibility/debugger/evaluating-a-watch-expression.md)
