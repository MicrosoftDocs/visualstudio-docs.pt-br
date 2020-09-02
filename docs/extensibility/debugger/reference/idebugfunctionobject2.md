---
title: IDebugFunctionObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c4150480d2e6686992d78727b6fed817da270145
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728435"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Representa uma função e aprimora a interface [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) .

## <a name="syntax"></a>Syntax

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um avaliador de expressão (EE) implementa essa interface para representar uma função.

## <a name="notes-for-callers"></a>Observações para chamadores
 Os métodos dessa interface adiam os de **IDebugFunctionObject** das seguintes maneiras:

- O método **IDebugEvaluate** usa sinalizadores.

- O método **CreateObject** usa sinalizadores e um tempo limite.

- O método **CreateStringObjectWithLength** usa um comprimento.

## <a name="methods"></a>Métodos
 Essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|Cria um objeto que usa um construtor de acordo com as configurações de sinalizador de avaliação e um valor de tempo limite.|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|Cria um objeto de cadeia de caracteres que tem o comprimento especificado.|
|[Avaliar](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|Chama a função e retorna o valor resultante como um objeto.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
