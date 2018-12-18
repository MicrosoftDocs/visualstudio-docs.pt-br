---
title: Exemplo de implementação da avaliação de expressão | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 10efa25ba2f692e9cf4a9c3588d210d31f9e8065
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49901288"
---
# <a name="sample-implementation-of-expression-evaluation"></a>Exemplo de implementação da avaliação de expressão
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [avaliador de expressão gerenciado exemplo](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Para um **Watch** expressão de janela, o Visual Studio chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para produzir um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto. `IDebugExpressionContext2::ParseText` cria uma instância de um avaliador de expressão (EE) e chama [analisar](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para obter uma [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) objeto.  
  
 O `IDebugExpressionEvaluator::Parse` realiza as seguintes tarefas:  
  
1.  [C++] Analisa a expressão para procurar erros.  
  
2.  Cria uma instância de uma classe (chamado `CParsedExpression` neste exemplo) que executa o `IDebugParsedExpression` de interface e o armazena na classe a expressão a ser analisado.  
  
3.  Retorna o `IDebugParsedExpression` da interface do `CParsedExpression` objeto.  
  
> [!NOTE]
>  Nos exemplos a seguir e, no exemplo MyCEE, o avaliador de expressão não separa a análise da avaliação.  
  
## <a name="managed-code"></a>Código gerenciado  
 O código a seguir mostra uma implementação de `IDebugExpressionEvaluator::Parse` em código gerenciado. Esta versão do método adia a análise para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) como o código para a análise também avalia ao mesmo tempo (consulte [avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)).  
  
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
O código a seguir é uma implementação de `IDebugExpressionEvaluator::Parse` em código não gerenciado. Este método chama uma função auxiliar, `Parse`, para analisar a expressão e verificar se há erros, mas esse método ignora o valor resultante. A avaliação formal é adiada para os [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) onde a expressão é analisada enquanto ela é avaliada (consulte [avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Avaliar uma expressão da janela de inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [Avaliar uma expressão de inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)