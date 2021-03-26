---
description: Essa interface representa uma função.
title: IDebugFunctionObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject
helpviewer_keywords:
- IDebugFunctionObject interface
ms.assetid: 8d94e97c-a9d1-400c-8a98-a44b5385b33a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0fabd43fe6f7d8ee8e5cddc6cc655088bf4a9abf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063546"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface representa uma função.

## <a name="syntax"></a>Sintaxe

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um avaliador de expressão implementa essa interface para representar uma função.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é uma especialização da interface [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) e é obtida usando [QueryInterface](/cpp/atl/queryinterface) na `IDebugObject` interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados de [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md), a `IDebugFunctionObject` interface expõe os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|Cria um objeto de dados primitivos.|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|Cria um objeto usando um construtor.|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|Cria um objeto sem Construtor.|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|Cria um objeto de matriz.|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|Cria um objeto de cadeia de caracteres.|
|[Avaliar](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|Chama a função e retorna o valor resultante como um objeto.|

## <a name="remarks"></a>Comentários
 Essa interface permite que o avaliador de expressão represente funções em uma árvore de análise. Os `Create` métodos nessa interface são usados para construir objetos que representam os parâmetros de entrada para o método. A função pode ser executada chamando o método [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) , que retorna um objeto que representa o valor retornado da função.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
