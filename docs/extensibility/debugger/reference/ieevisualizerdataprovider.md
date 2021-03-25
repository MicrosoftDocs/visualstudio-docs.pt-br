---
description: Essa interface fornece a capacidade de alterar o valor de um objeto por meio de um visualizador de tipo.
title: IEEVisualizerDataProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6af1f32a627b713c7907c9de29470f7624fdd7e4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080288"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface fornece a capacidade de alterar o valor de um objeto por meio de um visualizador de tipo.

## <a name="syntax"></a>Sintaxe

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O avaliador de expressão implementa essa interface para dar suporte à modificação de dados em um objeto de propriedade por meio de um visualizador de tipo.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é usada na criação do objeto [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) por meio de uma chamada para [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md). Consulte [visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter mais detalhes.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable

|Método|Descrição|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|Determina se é possível atualizar o objeto (e, subsequentemente, seu valor) que este visualizador está representando.|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|Força uma reavaliação do objeto para este visualizador.|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|Obtém um objeto existente para este visualizador (nenhuma avaliação é feita).|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|Atualiza o objeto para esse visualizador, alterando assim o valor que o visualizador apresenta.|

## <a name="remarks"></a>Comentários
 O serviço visualizador (conforme representado pela interface [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) e retornado por [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)) mantém uma referência ao objeto que implementa a `IEEVisualizerDataProvider` interface. Como resultado, a `IEEVisualizerDataProvider` interface não deve ser implementada no mesmo objeto que implementa o [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) se esse objeto mantém uma referência ao `IEEVisualizerService` objeto: um resultado de referência circular e um deadlock ocorre quando os objetos são destruídos. A abordagem recomendada é implementar `IEEVisualizerDataProvider` em um objeto separado para o qual o `IDebugProperty2` objeto Delega sem chamá `IUnknown::AddRef` -lo.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [Visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)
