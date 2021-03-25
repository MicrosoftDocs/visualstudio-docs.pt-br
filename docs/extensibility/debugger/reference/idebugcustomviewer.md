---
description: Essa interface permite que um avaliador de expressão (EE) exiba o valor de uma propriedade em qualquer formato necessário.
title: IDebugCustomViewer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c44706549d7d638a8fbf3686de57780ffa6bf4e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077545"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
Essa interface permite que um avaliador de expressão (EE) exiba o valor de uma propriedade em qualquer formato necessário.

## <a name="syntax"></a>Sintaxe

```
IDebugCustomViewer : IUknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
Um EE implementa essa interface para exibir o valor de uma propriedade em um formato personalizado.

## <a name="notes-for-callers"></a>Observações para chamadores
Uma chamada para a função do COM `CoCreateInstance` instancia essa interface. O `CLSID` passado para `CoCreateInstance` é obtido do registro. Uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) Obtém o local no registro. Consulte comentários para obter detalhes, bem como o exemplo.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
Essa interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|Faz tudo o que for necessário para exibir um determinado valor.|

## <a name="remarks"></a>Comentários
Essa interface é usada quando o valor de uma propriedade não pode ser exibido por meios normais — por exemplo, com uma tabela de dados ou outro tipo de propriedade complexo. Um visualizador personalizado, conforme representado pela `IDebugCustomViewer` interface, é diferente de um visualizador de tipo, que é um programa externo para exibir dados de um tipo específico, independentemente do EE. O EE implementa um visualizador personalizado que é específico daquele EE. Um usuário seleciona o tipo de visualizador a ser usado, seja um visualizador de tipo ou um visualizador personalizado. Consulte [visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes sobre esse processo.

Um visualizador personalizado é registrado da mesma maneira que um EE e, portanto, requer um GUID de idioma e um GUID de fornecedor. A métrica exata (ou o nome da entrada do registro) é conhecida apenas pelo EE. Essa métrica é retornada na estrutura de [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) , que, por sua vez, é retornada por uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md). O valor armazenado na métrica é o `CLSID` que é passado para a função de com `CoCreateInstance` (consulte o exemplo).

Os [auxiliares do SDK para a função de depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) , `SetEEMetric` , podem ser usados para registrar um visualizador personalizado. Consulte a seção de registro "avaliadores de expressão" de `Debugging SDK Helpers` para as chaves de registro específicas que um visualizador personalizado precisa. Observe que um visualizador personalizado precisa de apenas uma métrica (que é definida pelo implementador do EE), enquanto um avaliador de expressão requer várias métricas predefinidas.

Normalmente, um visualizador personalizado fornece uma exibição somente leitura dos dados, já que a interface [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) fornecida para [DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) não tem métodos para alterar o valor da propriedade, exceto como uma cadeia de caracteres. Para dar suporte à alteração de blocos de dados arbitrários, o EE implementa uma interface personalizada no mesmo objeto que implementa a `IDebugProperty3` interface. Essa interface personalizada forneceria os métodos necessários para alterar um bloco de dados arbitrário.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>Exemplo
Este exemplo mostra como obter o primeiro visualizador personalizado de uma propriedade se essa propriedade tiver qualquer visualizador personalizado.

```cpp
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)
{
    // This string is typically defined globally.  For this example, it
    // is defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugCustomViewer *pViewer = NULL;
    if (pProperty != NULL) {
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);
        if (pProperty3 != NULL) {
            HRESULT hr;
            ULONG viewerCount = 0;
            hr = pProperty3->GetCustomViewerCount(&viewerCount);
            if (viewerCount > 0) {
                ULONG viewersFetched = 0;
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };
                hr = pProperty3->GetCustomViewerList(0,
                                                     1,
                                                     &viewerInfo,
                                                     &viewersFetched);
                if (viewersFetched == 1) {
                    CLSID clsidViewer = { 0 };
                    CComPtr<IDebugCustomViewer> spCustomViewer;
                    // Get the viewer's CLSID from the registry.
                    ::GetEEMetric(viewerInfo.guidLang,
                                  viewerInfo.guidVendor,
                                  viewerInfo.bstrMetric,
                                  &clsidViewer,
                                  strRegistrationRoot);
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {
                        // Instantiate the custom viewer.
                        spCustomViewer.CoCreateInstance(clsidViewer);
                        if (spCustomViewer != NULL) {
                            pViewer = spCustomViewer.Detach();
                        }
                    }
                }
            }
        }
    }
    return(pViewer);
}
```

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
