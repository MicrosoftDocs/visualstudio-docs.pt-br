---
description: Essa interface fornece acesso a tipos, aliases e serviços personalizados de visualizador.
title: IDebugBinder3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29d8b642a66a75dd561b0a87cd5fa083e841139c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085150"
---
# <a name="idebugbinder3"></a>IDebugBinder3
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface fornece acesso a tipos, aliases e serviços personalizados de visualizador.

## <a name="syntax"></a>Sintaxe

```
IDebugBinder3 : IDebugBinder
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um mecanismo de depuração implementa essa interface para dar suporte a aliases, serviços de visualizador personalizado e acesso a informações de tipo de objeto.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma interface [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) obtém essa interface usando [QueryInterface](/cpp/atl/queryinterface).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos fornecidos pela interface [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) , essa interface implementa o seguinte:

|Método|Descrição|
|------------|-----------------|
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|Recupera um objeto de memória que representa a memória à qual esse objeto está associado.|
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|Recupera a exceção associada a este objeto (se houver),|
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|Recupera um alias de acordo com seu nome,|
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|Recupera uma matriz de todos os aliases para este objeto,|
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|Obtém o número de tipos de argumentos associados a este objeto,|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|Recupera uma lista de tipos de argumentos associados a este objeto,|
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|Obtém uma interface para um serviço visualizador,|
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|Converte um local de objeto ou um endereço de memória de 64 bits em um contexto de memória.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
