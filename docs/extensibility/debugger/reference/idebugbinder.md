---
title: IDebugBinder | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3514d280b6718fc670f3bdac35b6bbacbbf2b09c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31105090"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
>  No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão do CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface associa um campo de símbolo, normalmente é retornado pelo provedor de símbolo, em um contexto de memória ou um objeto que contém o valor atual do símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugBinder : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Esta interface dá suporte a avaliação de expressão e deve ser implementado pelo mecanismo de depuração (DE).  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é usado no processo de avaliação de expressão e normalmente é usado na implementação de [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) e [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugBinder`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Ligação](../../../extensibility/debugger/reference/idebugbinder-bind.md)|Obtém o contexto de memória ou um objeto que contém o valor atual do símbolo.|  
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|Determina o tipo de tempo de execução de um objeto.|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|Converte um endereço de memória ou local do objeto em um contexto de memória.|  
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|Obtém um [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) objeto usado para criar parâmetros de função.|  
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|Obtém o tipo exato de uma variável.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface retorna objetos que são usados pelo avaliador de expressão em árvores de análise. O avaliador de expressão analisa uma expressão, usando o provedor de símbolo para converter os símbolos na expressão em instâncias do [IDebugField](../../../extensibility/debugger/reference/idebugfield.md), que descrevem cada símbolo em termos de seu tipo e o local no código-fonte. O [associar](../../../extensibility/debugger/reference/idebugbinder-bind.md) método converte `IDebugField` objetos [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objetos que se conectar ou associar um símbolo de tipo para um valor real na memória. Essas `IDebugObject` objetos são armazenados em uma árvore de análise para avaliação posterior.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)   
 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)   
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)