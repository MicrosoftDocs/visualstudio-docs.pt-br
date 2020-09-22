---
title: Avaliando uma expressão Watch | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fd33a7c225e0cdc14ac3f1af9f4c78a7c1459615
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838309"
---
# <a name="evaluating-a-watch-expression"></a>Avaliando uma expressão de inspeção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Quando o Visual Studio está pronto para exibir o valor de uma expressão de inspeção, ele chama [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) que, por sua vez, chama [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md). Isso produz um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que contém o valor e o tipo da expressão.  
  
 Nessa implementação de `IDebugParsedExpression::EvaluateSync` , a expressão é analisada e avaliada ao mesmo tempo. Essa implementação executa as seguintes tarefas:  
  
1. Analisa e avalia a expressão para produzir um objeto genérico que contém o valor e seu tipo. Em C#, isso é representado como um `object` while em C++, que é representado como um `VARIANT` .  
  
2. Cria uma instância de uma classe (chamada `CValueProperty` neste exemplo) que implementa a `IDebugProperty2` interface e armazena na classe o valor a ser retornado.  
  
3. Retorna a `IDebugProperty2` interface do `CValueProperty` objeto.  
  
## <a name="managed-code"></a>Código gerenciado  
 Esta é uma implementação do `IDebugParsedExpression::EvaluateSync` em código gerenciado. O método auxiliar `Tokenize` analisa a expressão em uma árvore de análise. A função auxiliar `EvalToken` converte o token em um valor. A função auxiliar `FindTerm` percorre recursivamente a árvore de análise, chamando `EvalToken` para cada nó que representa um valor e aplicando quaisquer operações (adição ou subtração) na expressão.  
  
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
 Esta é uma implementação do `IDebugParsedExpression::EvaluateSync` em código não gerenciado. A função auxiliar `Evaluate` analisa e avalia a expressão, retornando uma `VARIANT` mantendo o valor resultante. A função auxiliar `VariantValueToProperty` agrupa o `VARIANT` em um `CValueProperty` objeto.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Avaliando uma expressão de janela de inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [Exemplo de implementação de avaliação de expressão](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
