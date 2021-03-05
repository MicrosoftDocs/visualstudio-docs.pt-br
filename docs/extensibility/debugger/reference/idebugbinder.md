---
description: Essa interface associa um campo de símbolo, normalmente retornado pelo provedor de símbolos, a um contexto de memória ou objeto que contém o valor atual do símbolo.
title: IDebugBinder | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: febe22338ddeaf275b37ae09c76921c91ec509da
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143617"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface associa um campo de símbolo, normalmente retornado pelo provedor de símbolos, a um contexto de memória ou objeto que contém o valor atual do símbolo.

## <a name="syntax"></a>Sintaxe

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Esta interface dá suporte à avaliação de expressão e deve ser implementada pelo mecanismo DE depuração (DE).

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é usada no processo de avaliação de expressão e normalmente é usada na implementação de [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) e [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugBinder` .

|Método|Descrição|
|------------|-----------------|
|[Associa](../../../extensibility/debugger/reference/idebugbinder-bind.md)|Obtém o contexto de memória ou o objeto que contém o valor atual do símbolo.|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|Determina o tipo de tempo de execução de um objeto.|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|Converte um local de objeto ou endereço de memória em um contexto de memória.|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|Obtém um objeto [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) usado para criar parâmetros de função.|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|Obtém o tipo exato para uma variável.|

## <a name="remarks"></a>Comentários
 Essa interface retorna objetos que são usados pelo avaliador de expressão em árvores de análise. O avaliador de expressão analisa uma expressão usando o provedor de símbolos para converter os símbolos na expressão em instâncias de [IDebugField](../../../extensibility/debugger/reference/idebugfield.md), que descrevem cada símbolo em termos de seu tipo e local no código-fonte. O método [BIND](../../../extensibility/debugger/reference/idebugbinder-bind.md) converte `IDebugField` objetos em objetos [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que se conectam ou associam um tipo de símbolo a um valor real na memória. Esses `IDebugObject` objetos são então armazenados em uma árvore de análise para avaliação posterior.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
