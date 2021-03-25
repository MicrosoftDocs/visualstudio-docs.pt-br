---
description: Essa interface representa uma propriedade de quadro de pilha, uma propriedade de documento de programa ou alguma outra propriedade.
title: IDebugProperty2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5d20f0bd3727860f32e111baad2d2513590e880
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064794"
---
# <a name="idebugproperty2"></a>IDebugProperty2
Essa interface representa uma propriedade de quadro de pilha, uma propriedade de documento de programa ou alguma outra propriedade. A propriedade é geralmente o resultado de uma avaliação de expressão.

> [!NOTE]
> Esse uso de "Property" não deve ser confundido com isso, o que significa uma variável de membro de uma classe, embora um `IDebugProperty2` possa representar essa entidade.

## <a name="syntax"></a>Sintaxe

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para representar um tipo específico de valor. Por exemplo, o valor pode ser um valor numérico como resultado de uma avaliação de expressão, um contexto de memória usado para exibir a memória ou uma lista de registradores e seus valores.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter essa interface, que representa o resultado de uma avaliação. `IDebugExpression2::EvaluateAsync` retorna essa interface enviando uma interface [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) para o SDM, que, por sua vez, chama [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) para recuperar a propriedade.

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) retorna essa interface para fornecer o documento de script associado.

- [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) retorna essa interface para representar o valor de retorno de uma função.

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) retorna essa interface para representar várias propriedades do programa, como um contexto de nome ou de memória.

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) retorna essa interface para representar várias propriedades do quadro de pilha, como variáveis locais.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProperty2` .

|Método|Descrição|
|------------|-----------------|
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|Preenche uma estrutura de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) que descreve uma propriedade.|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|Define o valor de uma propriedade de uma cadeia de caracteres.|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|Define o valor da propriedade a partir do valor de uma referência fornecida.|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|Enumera os filhos de uma propriedade.|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|Retorna o pai de uma propriedade.|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|Retorna a propriedade que descreve a propriedade mais derivada de uma propriedade.|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|Retorna os bytes de memória que compõem o valor de uma propriedade.|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|Retorna o contexto de memória para um valor de propriedade.|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|Retorna o tamanho, em bytes, do valor da propriedade.|
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|Retorna uma referência para o valor dessa propriedade.|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|Retorna as informações estendidas de uma propriedade.|

## <a name="remarks"></a>Comentários
 Uma propriedade, como representada por uma `IDebugProperty2` interface, pode ser considerada como um valor com um nome, um tipo e um endereço. Em termos mais gerais, um `IDebugProperty2` pode representar qualquer coisa que tenha uma estrutura hierárquica, com pais e nós filho.

 Normalmente, uma propriedade é transitória, o que dura apenas o período da pilha atual, por exemplo. Por outro lado, uma referência, como representada por uma interface [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) , dura desde que o valor permaneça na memória.

 O IDE pode usar a `IDebugProperty2` interface para permitir que os usuários procurem e modifiquem Propriedades em tempo de execução.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
