---
title: Exemplo de implementação da avaliação de expressão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a79f61351363ba14b9993181c77e1a9be88515d9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51735175"
---
# <a name="sample-implementation-of-expression-evaluation"></a>Exemplo de implementação de avaliação de expressão
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Para um **Watch** expressão de janela, o Visual Studio chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para produzir um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto. `IDebugExpressionContext2::ParseText` cria uma instância de um avaliador de expressão (EE) e chama [analisar](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para obter uma [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) objeto.  
  
 Essa implementação do `IDebugExpressionEvaluator::Parse` executa as seguintes tarefas:  
  
1.  [C++] Analisa a expressão para procurar erros.  
  
2.  Cria uma instância de uma classe (chamados `CParsedExpression` neste exemplo) que implementa o `IDebugParsedExpression` de interface e o armazena na classe a expressão a ser analisado.  
  
3.  Retorna o `IDebugParsedExpression` da interface do `CParsedExpression` objeto.  
  
> [!NOTE]
>  Nos exemplos a seguir e, no exemplo MyCEE, o avaliador de expressão não separa a análise da avaliação.  
  
## <a name="managed-code"></a>Código gerenciado  
 Essa é uma implementação de `IDebugExpressionEvaluator::Parse` em código gerenciado. Observe que esta versão do método adia a análise para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) como o código para a análise também avalia ao mesmo tempo (consulte [avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)).  
  
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
 Essa é uma implementação de `IDebugExpressionEvaluator::Parse` em código não gerenciado. Este método chama uma função auxiliar, `Parse`, para analisar a expressão e verificar se há erros, mas esse método ignora o valor resultante. A avaliação formal é adiada para os [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) onde a expressão é analisada enquanto ela é avaliada (consulte [avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)).  
  
```cpp#  
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
  
## <a name="see-also"></a>Consulte também  
 [Avaliar uma expressão da janela de inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [Avaliar uma expressão de Inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)

