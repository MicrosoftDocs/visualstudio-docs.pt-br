---
description: Essa interface representa um objeto de matriz.
title: IDebugArrayObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16162cee8a02bf02b192336425101ec4bb579106
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158521"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface representa um objeto de matriz.

## <a name="syntax"></a>Sintaxe

```
IDebugArrayObject : IDebugObject
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O avaliador de expressão implementa essa interface para representar uma matriz.

## <a name="notes-for-callers"></a>Observações para chamadores
 A interface [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) pode obter essa interface usando [QueryInterface](/cpp/atl/queryinterface) se o objeto representar uma matriz.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos na `IDebugObject` interface, os métodos a seguir são implementados na `IDebugArrayObject` interface.

|Método|Descrição|
|------------|-----------------|
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|Obtém a contagem de elementos na matriz.|
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|Obtém um elemento da matriz.|
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|Obtém todos os elementos da matriz.|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|Obtém a classificação da matriz.|
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|Obtém as dimensões da matriz.|

## <a name="remarks"></a>Comentários
 Um avaliador de expressão usa essa interface para representar matrizes em uma árvore de análise.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
