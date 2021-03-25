---
description: Representa um objeto de matriz gerenciado e permite que um avaliador de expressão (EE) determine o índice base (limites inferiores) para a matriz.
title: IDebugArrayObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugArrayObject2 interface
ms.assetid: be6e504d-4ab3-4141-a61b-0953ee0e038e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 169f4df61bcd4a58e74e0d83cee362b3926d2b36
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067563"
---
# <a name="idebugarrayobject2"></a>IDebugArrayObject2
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Representa um objeto de matriz gerenciado e permite que um avaliador de expressão (EE) determine o índice base (limites inferiores) para a matriz.

## <a name="syntax"></a>Sintaxe

```
IDebugArrayObject2 : IDebugArrayObject
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Isso é implementado pelo mecanismo DE depuração gerenciado (DE).

## <a name="methods"></a>Métodos
 Além dos métodos na interface [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) , essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-getbaseindices.md)|Recupera os índices de base (limites inferiores) para cada índice, considerando o número de dimensões na matriz.|
|[HasBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-hasbaseindices.md)|Determina se a matriz tem índices base (limites inferiores) definidos.|

## <a name="remarks"></a>Comentários
 Um avaliador de expressão usa essa interface para representar matrizes gerenciadas em uma árvore de análise.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
