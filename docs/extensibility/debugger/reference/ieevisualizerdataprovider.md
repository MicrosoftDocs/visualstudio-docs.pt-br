---
title: IEEVisualizerDataProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 269f154083f3589e989a6ca2f9ce0835b249181a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350186"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface fornece a capacidade de alterar o valor de um objeto por meio de um visualizador de tipo.

## <a name="syntax"></a>Sintaxe

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>Observações para implementadores
 O avaliador de expressão implementa essa interface para oferecer suporte a modificação dos dados em um objeto de propriedade por meio de um visualizador de tipo.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é usada na criação de [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) objeto por meio de uma chamada para [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md). Ver [visualização e exibindo os dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter mais detalhes.

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable

|Método|Descrição|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|Determina se é possível atualizar o objeto (e, depois, seu valor) que está representando esse visualizador.|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|Força uma reavaliação do objeto para este visualizador.|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|Obtém um objeto existente para este visualizador (nenhuma avaliação é feita).|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|Atualiza o objeto para esse visualizador, alterando assim o valor que apresenta o visualizador.|

## <a name="remarks"></a>Comentários
 O serviço de visualização simultânea (conforme representado pela [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) interface e retornado pelo [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)) mantém uma referência para o objeto que implementa o `IEEVisualizerDataProvider` interface . Como resultado, o `IEEVisualizerDataProvider` interface não deve ser implementado no mesmo objeto que implementa o [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) se esse objeto mantém uma referência para o `IEEVisualizerService` objeto: resultados de uma referência circular e uma deadlock ocorre quando os objetos são destruídos. A abordagem recomendada é implementar `IEEVisualizerDataProvider` em um objeto separado para o qual o `IDebugProperty2` objeto delegados sem chamar `IUnknown::AddRef` nele.

## <a name="requirements"></a>Requisitos
 Cabeçalho: ee.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Interfaces de Avaliação de Expressões](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [Visualizar e exibir dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)