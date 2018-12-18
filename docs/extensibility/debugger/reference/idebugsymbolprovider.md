---
title: IDebugSymbolProvider | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: de77e30f0e9f52af10eef1757048a078d6d4a583
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31121148"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
Essa interface representa um provedor de símbolo que fornece tipos, retornando-las como campos e símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugSymbolProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um provedor de símbolo deve implementar essa interface para fornecer o símbolo e informações para um avaliador de expressão de tipo.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é obtida por meio do COM `CoCreateInstance` função (por provedores de símbolo não gerenciado) ou carregando apropriada gerenciados assembly de código e criando o provedor de símbolo com base nas informações encontradas no assembly. O mecanismo de depuração instancia o provedor de símbolo para trabalhar em conjunto com o avaliador de expressão. Consulte o exemplo para uma abordagem para instanciar essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugSymbolProvider`.  
  
|Método|Descrição|  
|------------|-----------------|  
|`Initialize`|Preterido. Não use.|  
|`Uninitialize`|Preterido. Não use.|  
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|Obtém o campo que contém o endereço de depuração.|  
|`GetField`|Preterido. Não use.|  
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|Mapeia uma posição de documento em uma matriz de endereços de depuração.|  
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|Mapeia um contexto de documento em uma matriz de endereços de depuração.|  
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|Mapeia um endereço de depuração em um contexto de documento.|  
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|Obtém o idioma usado para compilar o código no endereço de depuração.|  
|`GetGlobalContainer`|Preterido. Não use.|  
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|Obtém o campo que representa um nome de método totalmente qualificado.|  
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|Obtém o tipo de campo de classe que representa um nome de classe totalmente qualificado.|  
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|Cria um enumerador para namespaces associado ao endereço de depuração.|  
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|Mapeia um nome de símbolo para um tipo de símbolo.|  
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|Obtém o endereço de depuração que segue um endereço de depuração fornecido em um método.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface mapeia as posições de documento em endereços de depuração e vice-versa.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como instanciar o provedor de símbolo, dado seu GUID (um mecanismo de depuração deve conhecer esse valor).  
  
```cpp  
// A debug engine uses its own symbol provider and would know the GUID  
// of that provider.  
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)  
{  
    // This is typically defined globally.  For this example, it is  
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
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de Provedor de Símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)