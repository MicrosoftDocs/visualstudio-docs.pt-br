---
title: IDebugCustomViewer | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6b9e068591961e7eafa9d4fdc588da2694532463
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759507"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface permite que um avaliador de expressão (EE) para exibir um valor de propriedade em qualquer formato que é necessário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCustomViewer : IUknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um EE implementa essa interface para exibir um valor de propriedade em um formato personalizado.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Uma chamada ao COM `CoCreateInstance` função cria uma instância dessa interface. O `CLSID` passado para `CoCreateInstance` é obtido do registro. Uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) obtém o local no registro. Consulte os comentários para obter detalhes, bem como o exemplo.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Essa interface implementa o método a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|Faz o que for necessário para exibir um determinado valor.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é usada quando o valor da propriedade não pode ser exibido por meios normais — por exemplo, com uma tabela de dados ou outro tipo de propriedade complexa. Um visualizador personalizado, conforme representado pelo `IDebugCustomViewer` interface, é diferente de um visualizador de tipo, que é um programa externo para exibir dados de um tipo específico, independentemente do EE. O EE implementa um visualizador personalizado que é específico para esse EE. Um usuário seleciona qual tipo de visualização simultânea para usar, seja ele um visualizador de tipo ou um visualizador personalizado. Ver [visualização e exibindo os dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes sobre esse processo.  
  
 Um visualizador personalizado está registrado da mesma forma como um EE e, portanto, requer uma linguagem de GUID e um GUID do fornecedor. A métrica exata (ou o nome da entrada do registro) é conhecido apenas o EE. Essa métrica é retornada na [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) estrutura, que por sua vez, é retornada por uma chamada para [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md). O valor armazenado na métrica é a `CLSID` que é passada para o do COM `CoCreateInstance` funcionar (consulte o exemplo).  
  
 O [auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) função, `SetEEMetric`, pode ser usado para registrar um visualizador personalizado. Consulte a seção do Registro "Avaliadores de expressão" `Debugging SDK Helpers` para chaves de registro específico que precisa de um visualizador personalizado. Observe que um visualizador personalizado precisa apenas uma métrica (que é definida pelo implementador do EE) enquanto um avaliador de expressão requer várias métricas predefinidas.  
  
 Normalmente, um visualizador personalizado fornece uma exibição somente leitura dos dados, desde o [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) interface fornecido à [DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) não tem métodos para alterar o valor da propriedade, exceto como uma cadeia de caracteres. Para dar suporte a blocos arbitrários de dados de alteração, o EE implementa uma interface personalizada no mesmo objeto que implementa o `IDebugProperty3` interface. Essa interface personalizada deve fornecer os métodos necessários para alterar um bloco arbitrário de dados.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como obter o primeiro visualizador personalizado de uma propriedade, se essa propriedade tiver qualquer visualizadores personalizados.  
  
```cpp#  
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
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)

