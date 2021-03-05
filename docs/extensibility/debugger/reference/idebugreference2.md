---
description: Essa interface representa uma referência a uma propriedade de quadro de pilha ou alguma outra propriedade.
title: IDebugReference2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 04d9795388b2a079d0eb7ac1d787bf92de6cdff4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165846"
---
# <a name="idebugreference2"></a>IDebugReference2
Essa interface representa uma referência a uma propriedade de quadro de pilha ou alguma outra propriedade.

> [!NOTE]
> `IDebugReference2` é reservado para uso futuro e todos os seus métodos devem retornar `E_NOTIMPL` .

## <a name="syntax"></a>Sintaxe

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para representar uma referência a um tipo específico de valor. Por exemplo, o valor pode ser um valor numérico como resultado de uma avaliação de expressão, um contexto de memória usado para exibir a memória ou uma lista de registradores e seus valores.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [getReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md) para obter essa interface. [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md) e [GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md) também retornam essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugReference2` .

|Método|Descrição|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|Obtém a estrutura de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) que descreve essa referência.|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|Define o valor dessa referência a partir de uma cadeia de caracteres.|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|Define o valor dessa referência de outra referência.|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|Enumera os filhos dessa referência.|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|Obtém o pai desta referência.|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|Obtém a referência mais derivada dessa referência.|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|Obtém os bytes de memória aos quais essa referência se refere.|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|Obtém um contexto de memória para esta referência.|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|Obtém o tamanho, em bytes, dessa referência.|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|Define esse tipo de referência.|
|[Comparar](../../../extensibility/debugger/reference/idebugreference2-compare.md)|Compara esta referência com outra.|

## <a name="remarks"></a>Comentários

> [!NOTE]
> Esse uso de "Property" não deve ser confundido com isso, o que significa uma variável de membro de uma classe, embora um `IDebugReference2` possa representar essa entidade.

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) representa uma propriedade, enquanto `IDebugReference2` representa uma referência a uma propriedade, normalmente uma referência a um objeto no programa que está sendo depurado.

 A principal diferença entre uma propriedade e uma referência é que uma propriedade se refere a uma instância nomeada de um objeto, enquanto uma referência se refere a uma instância sem nome. Por exemplo, uma propriedade pode se referir a um objeto no heap do programa pelo `"a.b"` . Outra propriedade pode se referir ao mesmo objeto que `"c.d"` . A maneira de fazer referência a essa propriedade requer que `"a.b"` ou `"c.d"` esteja no escopo. Uma referência a esse mesmo objeto é sem nome; o objeto pode ser referenciado desde que a memória para esse objeto seja válida.

 Uma `IDebugProperty2` interface pode ser considerada como um valor com um nome, um tipo e um endereço. Um `IDebugReference2` , por outro lado, pode ser considerado um tipo e um endereço.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
