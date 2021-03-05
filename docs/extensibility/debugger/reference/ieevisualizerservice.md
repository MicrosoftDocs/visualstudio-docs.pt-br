---
description: Essa interface implementa os principais métodos que fornecem funcionalidade às interfaces IDebugProperty3 e IPropertyProxyEESide.
title: IEEVisualizerService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService
helpviewer_keywords:
- IEEVisualizerService interface
ms.assetid: 3bdb124b-c582-47ba-b465-13c6a1cdb702
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5054041ab09898943d300393d36205581231b06d
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102227210"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface implementa os principais métodos que fornecem funcionalidade às interfaces [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) e [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) .

## <a name="syntax"></a>Sintaxe

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio implementa essa interface para permitir que um avaliador de expressão (EE) dê suporte a visualizadores de tipo.

## <a name="notes-for-callers"></a>Observações para chamadores
 O EE chama [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) para obter essa interface como parte de seu suporte para visualizadores de tipo.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable

|Método|Descrição|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|Recupera o número de visualizadores personalizados sobre os quais esse serviço sabe.|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|Recupera a lista de visualizadores personalizados.|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|Retorna um objeto proxy para uma propriedade.|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|Recupera o número de cadeias de caracteres de valor a serem exibidas para a propriedade ou o campo especificado.|

## <a name="remarks"></a>Comentários
 O IDE usa a interface [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) para determinar se há algum visualizador personalizado ou Visualizar tipo para a propriedade. Ao criar um serviço visualizador (com [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)), o EE pode fornecer a funcionalidade para o `IDebugProperty3` e o [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) (que dá suporte à exibição e alteração de interfaces de valor de uma propriedade) e, portanto, suporte a visualizadores de tipo.

 Se um EE tiver visualizadores personalizados implementados por si só, o EE poderá acrescentar os `CLSID` s desses visualizadores personalizados ao final da lista retornada por [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md). Isso permite que um EE ofereça suporte a visualizadores de tipo e seus próprios visualizadores personalizados. Apenas certifique-se de que [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) reflete a adição de qualquer visualizador personalizado.

 Consulte Visualizador de [tipos e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) para obter uma discussão sobre a diferença entre visualizadores e visualizadores.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [Visualizador de tipo e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
