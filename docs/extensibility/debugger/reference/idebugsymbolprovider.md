---
description: Essa interface representa um provedor de símbolos que fornece símbolos e tipos, retornando-os como campos.
title: IDebugSymbolProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0488520f8bde0ccd2638636810cb0055a7f3f4b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168420"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
Essa interface representa um provedor de símbolos que fornece símbolos e tipos, retornando-os como campos.

## <a name="syntax"></a>Sintaxe

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
Um provedor de símbolo deve implementar essa interface para fornecer informações de símbolo e tipo a um avaliador de expressão.

## <a name="notes-for-callers"></a>Observações para chamadores
Essa interface é obtida usando `CoCreateInstance` a função de com (para provedores de símbolos não gerenciados) ou carregando o assembly de código gerenciado apropriado e instanciando o provedor de símbolos com base nas informações encontradas nesse assembly. O mecanismo de depuração instancia o provedor de símbolos para trabalhar em coordenação com o avaliador de expressão. Consulte o exemplo de uma abordagem para instanciar essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDebugSymbolProvider` .

|Método|Descrição|
|------------|-----------------|
|`Initialize`|Preterido. Não use.|
|`Uninitialize`|Preterido. Não use.|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|Obtém o campo que contém o endereço de depuração.|
|`GetField`|Preterido. Não use.|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|Mapeia uma posição de documento em uma matriz de endereços de depuração.|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|Mapeia um contexto de documento em uma matriz de endereços de depuração.|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|Mapeia um endereço de depuração em um contexto de documento.|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|Obtém a linguagem usada para compilar o código no endereço de depuração.|
|`GetGlobalContainer`|Preterido. Não use.|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|Obtém o campo que representa um nome de método totalmente qualificado.|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|Obtém o tipo de campo de classe que representa um nome de classe totalmente qualificado.|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|Cria um enumerador para namespaces associados ao endereço de depuração.|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|Mapeia um nome de símbolo para um tipo de símbolo.|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|Obtém o endereço de depuração que segue um determinado endereço de depuração em um método.|

## <a name="remarks"></a>Comentários
Essa interface mapeia as posições do documento em endereços de depuração e vice-versa.

## <a name="requirements"></a>Requisitos
Cabeçalho: sh. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>Exemplo
Este exemplo mostra como criar uma instância do provedor de símbolos, dado seu GUID (um mecanismo de depuração deve saber esse valor).

```cpp
// A debug engine uses its own symbol provider and would know the GUID
// of that provider.
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugSymbolProvider *pProvider = NULL;
    if (pSymbolProviderGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetSPMetric(*pSymbolProviderGuid,
                      storetypeFile,
                      metricCLSID,
                      &clsidProvider,
                      strRegistrationRoot);
        if (IsEqualGUID(clsidProvider,GUID_NULL)) {
            // No file type provider, try metadata provider.
            ::GetSPMetric(*pSymbolProviderGuid,
                          ::storetypeMetadata,
                          metricCLSID,
                          &clsidProvider,
                          strRegistrationRoot);
        }
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugSymbolProvider> spSymbolProvider;
            spSymbolProvider.CoCreateInstance(clsidProvider);
            if (spSymbolProvider != NULL) {
                pProvider = spSymbolProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
