---
title: Avaliar uma expressão de inspeção | Microsoft Docs
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
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 89cc466ee06cd0b4834a03495088c2efdc749e5a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780289"
---
# <a name="evaluating-a-watch-expression"></a>Avaliando uma expressão de inspeção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Quando o Visual Studio está pronto para exibir o valor de uma expressão de inspeção, ele chama [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) que por sua vez chama [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md). Isso produz um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto que contém o valor e o tipo da expressão.  
  
 Nessa implementação de `IDebugParsedExpression::EvaluateSync`, a expressão é analisada e avaliada ao mesmo tempo. Esta implementação realiza as seguintes tarefas:  
  
1.  Analisa e avalia a expressão para produzir um objeto genérico que contém o valor e seu tipo. No c#, isso é representado como uma `object` enquanto em C++ é representado como um `VARIANT`.  
  
2.  Cria uma instância de uma classe (chamados `CValueProperty` neste exemplo) que implementa o `IDebugProperty2` de interface e o armazena na classe de valor a ser retornado.  
  
3.  Retorna o `IDebugProperty2` da interface do `CValueProperty` objeto.  
  
## <a name="managed-code"></a>Código gerenciado  
 Essa é uma implementação do `IDebugParsedExpression::EvaluateSync` em código gerenciado. O método auxiliar `Tokenize` analisa a expressão em uma árvore de análise. A função auxiliar `EvalToken` converte o token para um valor. A função auxiliar `FindTerm` recursivamente percorre a árvore de análise, chamar `EvalToken` para cada nó que representa um valor e a aplicação de qualquer operação (adição ou subtração) na expressão.  
  
```csharp  
namespace EEMC  
{  
    public class CParsedExpression : IDebugParsedExpression  
    {  
        public HRESULT EvaluateSync(  
            uint evalFlags,  
            uint timeout,  
            IDebugSymbolProvider provider,  
            IDebugAddress address,  
            IDebugBinder binder,  
            string resultType,  
            out IDebugProperty2 result)  
        {  
            HRESULT retval = COM.S_OK;  
            this.evalFlags = evalFlags;  
            this.timeout = timeout;  
            this.provider = provider;  
            this.address = address;  
            this.binder = binder;  
            this.resultType = resultType;  
  
            try  
            {  
                IDebugField field = null;  
                // Tokenize, then parse.  
                tokens = Tokenize(expression);  
                result = new CValueProperty(  
                             expression,  
                             (int) FindTerm(EvalToken(tokens[0], out field),1),  
                             field,  
                             binder);  
            }  
            catch (ParseException)  
            {  
                result = new CValueProperty(expression, "Huh?");  
                retval = COM.E_INVALIDARG;  
            }  
            return retval;  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code"></a>Código não gerenciado  
 Essa é uma implementação do `IDebugParsedExpression::EvaluateSync` em código não gerenciado. A função auxiliar `Evaluate` analisa e avalia a expressão, retornando um `VARIANT` que contém o valor resultante. A função auxiliar `VariantValueToProperty` pacotes do `VARIANT` em um `CValueProperty` objeto.  
  
```  
[C++]  
STDMETHODIMP CParsedExpression::EvaluateSync(   
    in  DWORD                 evalFlags,  
    in  DWORD                 dwTimeout,  
    in  IDebugSymbolProvider* pprovider,  
    in  IDebugAddress*        paddress,  
    in  IDebugBinder*         pbinder,  
    in  BSTR                  bstrResultType,  
    out IDebugProperty2**     ppproperty )  
{  
    // dwTimeout parameter is ignored in this implementation.  
    if (pprovider == NULL)  
        return E_INVALIDARG;  
  
    if (paddress == NULL)  
        return E_INVALIDARG;  
  
    if (pbinder == NULL)  
        return E_INVALIDARG;  
  
    if (ppproperty == NULL)  
        return E_INVALIDARG;  
    else  
        *ppproperty = 0;  
  
    HRESULT hr;  
    VARIANT value;  
    BSTR    bstrErrorMessage = NULL;  
    hr = ::Evaluate( pprovider,  
                     paddress,  
                     pbinder,  
                     m_expr,  
                     &bstrErrorMessage,  
                     &value );  
    if (hr != S_OK)  
    {  
        if (bstrErrorMessage == NULL)  
            return hr;  
  
        //we can display better messages ourselves.  
        HRESULT hrLocal = S_OK;  
        VARIANT varType;  
        VARIANT varErrorMessage;  
  
        VariantInit( &varType );  
        VariantInit( &varErrorMessage );  
        varErrorMessage.vt      = VT_BSTR;  
        varErrorMessage.bstrVal = bstrErrorMessage;  
  
        CValueProperty* valueProperty = new CValueProperty();  
        if (valueProperty != NULL)  
        {  
            hrLocal = valueProperty->Init(m_expr, varType, varErrorMessage);  
            if (SUCCEEDED(hrLocal))   
            {  
                hrLocal = valueProperty->QueryInterface( IID_IDebugProperty2,  
                        reinterpret_cast<void**>(ppproperty) );  
            }  
        }  
  
        VariantClear(&varType);  
        VariantClear(&varErrorMessage); //frees BSTR  
        if (!valueProperty)  
            return hr;  
        valueProperty->Release();  
        if (FAILED(hrLocal))  
            return hr;  
    }  
    else  
    {  
        if (bstrErrorMessage != NULL)  
            SysFreeString(bstrErrorMessage);  
  
        hr = VariantValueToProperty( pprovider,  
                                     paddress,  
                                     pbinder,  
                                     m_radix,  
                                     m_expr,  
                                     value,  
                                     ppproperty );  
        VariantClear(&value);  
        if (FAILED(hr))  
            return hr;  
    }  
  
    return S_OK;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Avaliar uma expressão da janela de inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [Exemplo de implementação da Avaliação de expressão](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)

