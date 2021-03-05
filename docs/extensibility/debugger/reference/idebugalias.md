---
description: Representa um alias numérico para uma variável.
title: IDebugAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fd5639c510ba5a4a346c7a6f2630e7f14ddf036
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143877"
---
# <a name="idebugalias"></a>IDebugAlias
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Representa um alias numérico para uma variável. Um alias é simplesmente um nome diferente para uma variável.

## <a name="syntax"></a>Sintaxe

```
IDebugAlias : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O avaliador de expressão (EE) implementa essa interface para dar suporte a aliases numéricos para variáveis.

## <a name="notes-for-callers"></a>Observações para chamadores
- [Createalias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) cria um alias para um objeto específico. Para procurar aliases, use [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md) ou [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Os métodos a seguir são definidos na `IDebugAlias` interface.

|Método|Descrição|
|------------|-----------------|
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|Obtém o objeto ao qual este alias se refere.|
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|Obtém o nome do alias.|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|Recupera uma `ICorDebugValue` interface que fornece acesso a informações de código gerenciado sobre este objeto (somente código gerenciado).|
|[Dispose](../../../extensibility/debugger/reference/idebugalias-dispose.md)|Marca este alias como não sendo mais usado.|

## <a name="remarks"></a>Comentários
 Um alias é um número decimal na forma de cadeia de caracteres seguido pelo caractere #, por exemplo, 1001 #.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)
- [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)
- [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
