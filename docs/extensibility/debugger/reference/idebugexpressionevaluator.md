---
description: Essa interface representa o avaliador de expressão.
title: IDebugExpressionEvaluator | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b2e1fb465155bac2aa4be2b0d0a041715bf63bfa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152345"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

Essa interface representa o avaliador de expressão.

## <a name="syntax"></a>Sintaxe

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
O avaliador de expressão deve implementar essa interface.

## <a name="notes-for-callers"></a>Observações para chamadores
Para obter essa interface, crie uma instância do avaliador de expressão por meio do `CoCreateInstance` método usando a ID de classe (CLSID) do avaliador. Consulte o exemplo.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDebugExpressionEvaluator` .

|Método|Descrição|
|------------|-----------------|
|[Analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|Converte uma cadeia de caracteres de expressão em uma expressão analisada.|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|Obtém as variáveis locais, os argumentos e outras propriedades de um método.|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|Converte um local de método e um deslocamento em um endereço de memória.|
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|Determina qual idioma usar para criar resultados imprimíveis.|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|Define a raiz do registro. Usado para depuração lado a lado.|

## <a name="remarks"></a>Comentários
Em uma situação típica, o mecanismo de depuração (DE) cria uma instância do avaliador de expressão (EE) como resultado de uma chamada para [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md). Como o de conhece a linguagem e o fornecedor do EE que deseja usar, o DE Obtém o CLSID do registro (os [auxiliares do SDK para a função de depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) , `GetEEMetric` , ajuda com essa recuperação).

Depois que o EE é instanciado, o DE chama [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para analisar a expressão e armazená-la em um objeto [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) . Posteriormente, uma chamada para [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) avalia a expressão.

## <a name="requirements"></a>Requisitos
Cabeçalho: EE. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>Exemplo
Este exemplo mostra como criar uma instância do avaliador de expressão, dado um provedor de símbolos e um endereço no código-fonte. Este exemplo usa uma função, `GetEEMetric` , dos [auxiliares do SDK para depurar a](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) biblioteca, dbgmetric. lib.

```cpp
IDebugExpressionEvaluator GetExpressionEvaluator(IDebugSymbolProvider pSymbolProvider,
                                                 IDebugAddress *pSourceAddress)
{
    // This is typically defined globally but is specified here just
    // for this example.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";

    IDebugExpressionEvaluator *pEE = NULL;
    if (pSymbolProvider != NULL && pSourceAddress != NULL) {
        HRESULT hr         = S_OK;
        GUID  languageGuid = { 0 };
        GUID  vendorGuid   = { 0 };

        hr = pSymbolProvider->GetLanguage(pSourceAddress,
                                          &languageGuid,
                                          &vendorGuid);
        if (SUCCEEDED(hr)) {
            CLSID clsidEE = { 0 };
            CComPtr<IDebugExpressionEvaluator> spExpressionEvaluator;
            // Get the expression evaluator's CLSID from the registry.
            ::GetEEMetric(languageGuid,
                          vendorGuid,
                          metricCLSID,
                          &clsidEE,
                          strRegistrationRoot);
            if (!IsEqualGUID(clsidEE,GUID_NULL)) {
                // Instantiate the expression evaluator.
                spExpressionEvaluator.CoCreateInstance(clsidEE);
            }
            if (spExpressionEvaluator != NULL) {
                pEE = spExpressionEvaluator.Detach();
            }
        }
    }
    return pEE;
}
```

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
