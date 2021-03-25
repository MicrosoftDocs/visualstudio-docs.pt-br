---
description: Essa interface permite que o avaliador de expressão (EE) chame Propriedades ou métodos em instâncias de classe de valor (por exemplo, System. decimal) e defina seu valor sem chamar Evaluate no programa que está sendo depurado.
title: IDebugManagedObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88eadb33aaccc09a7c4667ad01d9acee538169f2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076856"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface permite que o avaliador de expressão (EE) chame Propriedades ou métodos em instâncias de classe de valor (por exemplo, `System.Decimal` ) e defina seu valor sem chamar [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) no programa que está sendo depurado.

## <a name="syntax"></a>Sintaxe

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um avaliador de expressão implementa essa interface para representar um objeto de código gerenciado, como uma variável.

## <a name="notes-for-callers"></a>Observações para chamadores
 Para obter essa interface, chame [GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md) em um [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa uma instância de uma classe Value.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados de [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md), a `IDebugManagedObject` interface expõe os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|Retorna uma interface que representa o objeto de código gerenciado e do qual qualquer interface de código gerenciada apropriada pode ser obtida.|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|Define o valor desse objeto como o valor de um objeto de código gerenciado especificado.|

## <a name="remarks"></a>Comentários
 Um avaliador de expressão usa essa interface para armazenar um objeto de código gerenciado em uma árvore de análise.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Avaliar](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
