---
title: Implementando getmethodproperty | Microsoft Docs
description: Saiba como o Visual Studio obtém informações sobre o método atual no quadro de pilha usando o getdebugproperty do mecanismo de depuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ab7b0ba5e51ba8ea47b473934e825b82dec320c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903288"
---
# <a name="implement-getmethodproperty"></a>Implementar getmethodproperty
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

O Visual Studio chama o (DE) [Getdebugproperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)do mecanismo de depuração, que, por sua vez, chama [getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) para obter informações sobre o método atual no quadro de pilha.

Essa implementação do `IDebugExpressionEvaluator::GetMethodProperty` executa as seguintes tarefas:

1. Chama [Getcontainerfield](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md), passando o objeto [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) . O provedor de símbolos (SP) retorna um [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) que representa o método que contém o endereço especificado.

2. Obtém o [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) do `IDebugContainerField` .

3. Cria uma instância de uma classe (chamada `CFieldProperty` neste exemplo) que implementa a interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) e contém o `IDebugMethodField` objeto retornado do SP.

4. Retorna a `IDebugProperty2` interface do `CFieldProperty` objeto.

## <a name="managed-code"></a>Código gerenciado
Este exemplo mostra uma implementação do `IDebugExpressionEvaluator::GetMethodProperty` em código gerenciado.

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        public HRESULT GetMethodProperty(
                IDebugSymbolProvider symbolProvider,
                IDebugAddress        address,
                IDebugBinder         binder,
                int                  includeHiddenLocals,
            out IDebugProperty2      property)
        {
            IDebugContainerField containerField = null;
            IDebugMethodField methodField       = null;
            property = null;

            // Get the containing method field.
            symbolProvider.GetContainerField(address, out containerField);
            methodField = (IDebugMethodField) containerField;

            // Return the property of method field.
            property = new CFieldProperty(symbolProvider, address, binder, methodField);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>Código não gerenciado
Este exemplo mostra uma implementação de `IDebugExpressionEvaluator::GetMethodProperty` em código não gerenciado.

```
[CPP]
STDMETHODIMP CExpressionEvaluator::GetMethodProperty(
        in IDebugSymbolProvider *pprovider,
        in IDebugAddress        *paddress,
        in IDebugBinder         *pbinder,
        in BOOL                  includeHiddenLocals,
        out IDebugProperty2    **ppproperty
    )
{
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    IDebugContainerField* pcontainer = NULL;

    hr = pprovider->GetContainerField(paddress, &pcontainer);
    if (FAILED(hr))
        return hr;

    IDebugMethodField*    pmethod    = NULL;
    hr = pcontainer->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod));
    pcontainer->Release();
    if (FAILED(hr))
        return hr;

    CFieldProperty* pfieldProperty = new CFieldProperty( pprovider,
                                                         paddress,
                                                         pbinder,
                                                         pmethod );
    pmethod->Release();
    if (!pfieldProperty)
        return E_OUTOFMEMORY;

    hr = pfieldProperty->Init();
    if (FAILED(hr))
    {
        pfieldProperty->Release();
        return hr;
    }

    hr = pfieldProperty->QueryInterface( IID_IDebugProperty2,
            reinterpret_cast<void**>(ppproperty));
    pfieldProperty->Release();

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [Exemplo de implementação de locais](../../extensibility/debugger/sample-implementation-of-locals.md)
