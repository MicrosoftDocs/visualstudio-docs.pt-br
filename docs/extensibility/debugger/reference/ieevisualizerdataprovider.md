---
title: IEEVisualizerDataProvider | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8e37561957d592ecd9ae855f2816c860f84e7b20
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31121216"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
>  No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão do CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface fornece a capacidade de alterar o valor de um objeto por meio de um visualizador de tipo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEEVisualizerDataProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O avaliador de expressão implementa essa interface para oferecer suporte a modificação dos dados em um objeto de propriedade por meio de um visualizador de tipo.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é usada na criação de [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) objeto por meio de uma chamada para [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md). Consulte [Visualizing e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter mais detalhes.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|Determina se é possível atualizar o objeto (e posteriormente, seu valor) que este visualizador está representando.|  
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|Força uma reavaliação do objeto para este visualizador.|  
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|Obtém um objeto existente para este visualizador (nenhuma avaliação é feita).|  
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|Atualiza o objeto para esse visualizador, alterando assim o valor que apresenta o visualizador.|  
  
## <a name="remarks"></a>Comentários  
 O serviço do visualizador (conforme representado pelo [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) interface e retornado por [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)) mantém uma referência para o objeto que implementa o `IEEVisualizerDataProvider` interface . Como resultado, o `IEEVisualizerDataProvider` interface não deve ser implementada no mesmo objeto que implementa o [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) se esse objeto mantém uma referência para o `IEEVisualizerService` objeto: resultados de uma referência circular e um deadlock ocorre quando os objetos são destruídos. A abordagem recomendada é implementar `IEEVisualizerDataProvider` em um objeto separado no qual o `IDebugProperty2` objeto delegados sem chamar `IUnknown::AddRef` nele.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)   
 [Visualizar e exibir dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)