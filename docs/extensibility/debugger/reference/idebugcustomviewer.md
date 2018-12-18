---
title: IDebugCustomViewer | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3fb70365304883abe99a87cfec5e78bbed89f2dd
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31107534"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
Essa interface permite que um avaliador de expressão (EE) para exibir um valor de propriedade em qualquer formato que é necessário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCustomViewer : IUknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um EE implementa essa interface para exibir um valor de propriedade em um formato personalizado.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Uma chamada para COM `CoCreateInstance` função instancia nesta interface. O `CLSID` passado para `CoCreateInstance` é obtido do registro. Uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) obtém o local no registro. Consulte comentários para obter detalhes, bem como o exemplo.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Essa interface implementa o método a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|Faz o que for necessário para exibir um determinado valor.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é usada quando o valor da propriedade não pode ser exibido por meios normais — por exemplo, com uma tabela de dados ou outro tipo de propriedade complexa. Um visualizador personalizado, representados pelo `IDebugCustomViewer` interface, que é diferente de um visualizador de tipo, que é um programa externo para exibir dados de um tipo específico, independentemente do EE. O EE implementa um visualizador personalizado que é específico para esse EE. Um usuário seleciona o tipo de visualizador para usar, seja ele um visualizador de tipo ou um visualizador personalizado. Consulte [Visualizing e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes sobre esse processo.  
  
 Um visualizador personalizado é registrado da mesma forma como um EE e, portanto, requer um idioma GUID e um fornecedor de GUID. A métrica exata (ou o nome da entrada do registro) é conhecido apenas o EE. Essa métrica é retornada no [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) estrutura, que por sua vez, é retornada por uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md). O valor armazenado na métrica é o `CLSID` que é passado para COM `CoCreateInstance` função (veja o exemplo).  
  
 O [auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) função, `SetEEMetric`, pode ser usado para registrar um visualizador personalizado. Consulte a seção do Registro "Avaliadores de expressão" `Debugging SDK Helpers` para chaves de registro específico que precisa de um visualizador personalizado. Observe que um visualizador personalizado precisa apenas uma métrica (que é definida por implementador da EE) enquanto um avaliador de expressão requer várias métricas predefinidas.  
  
 Normalmente, um visualizador personalizado fornece uma exibição somente leitura dos dados, como o [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) interface fornecida para [DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) não possui métodos para alterar o valor da propriedade exceto como uma cadeia de caracteres. Para oferecer suporte a alteração arbitrários blocos de dados, o EE implementa uma interface personalizada no mesmo objeto que implementa o `IDebugProperty3` interface. Essa interface personalizada ofereceria, em seguida, os métodos necessários para alterar um bloco arbitrário de dados.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como obter o primeiro visualizador personalizado de uma propriedade, se essa propriedade tem qualquer visualizadores personalizados.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)