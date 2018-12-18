---
title: IDebugProperty2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fb0cd134d30da277ddc1f984e0cf9e57dd5e4963
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31121567"
---
# <a name="idebugproperty2"></a>IDebugProperty2
Essa interface representa uma propriedade de quadro de pilha, uma propriedade de documento do programa ou outra propriedade. A propriedade normalmente é o resultado de uma avaliação de expressão.  
  
> [!NOTE]
>  Esse uso de "property" não deve ser confundido com que uma variável de membro de uma classe, significando que embora um `IDebugProperty2` pode representar a essa entidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProperty2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O DE implementa essa interface para representar um determinado tipo de valor. Por exemplo, o valor pode ser um valor numérico como resultado de uma avaliação de expressão, um contexto de memória usado para exibir a memória ou uma lista de registros e seus valores.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamar [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter essa interface, que representa o resultado de uma avaliação. `IDebugExpression2::EvaluateAsync` Retorna a essa interface, enviando um [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) interface SDM, que por sua vez, chama [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) ao recuperar a propriedade.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) retorna essa interface para fornecer o documento de script associados.  
  
 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) retorna essa interface para representar o valor de retorno de uma função.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) retorna essa interface para representar várias propriedades do programa, como um nome ou um contexto de memória.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) retorna essa interface para representar várias propriedades do quadro de pilhas como variáveis locais.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugProperty2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|Preenche uma [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estrutura que descreve uma propriedade.|  
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|Define o valor de uma propriedade de uma cadeia de caracteres.|  
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|Define o valor da propriedade do valor de uma determinada referência.|  
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|Enumera os filhos de uma propriedade.|  
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|Retorna o pai de uma propriedade.|  
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|Retorna a propriedade que descreve a propriedade mais derivado de uma propriedade.|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|Retorna os bytes de memória que compõem o valor de uma propriedade.|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|Retorna o contexto de memória para um valor de propriedade.|  
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|Retorna o tamanho, em bytes, do valor da propriedade.|  
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|Retorna uma referência para o valor desta propriedade.|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|Retorna as informações estendidas de uma propriedade.|  
  
## <a name="remarks"></a>Comentários  
 Uma propriedade, conforme representado por um `IDebugProperty2` interface, pode ser pensada como um valor com um nome, um tipo e um endereço. Em termos mais gerais, um `IDebugProperty2` pode representar qualquer coisa que tenha uma estrutura hierárquica, com os pais e os nós filho.  
  
 Uma propriedade é geralmente transitório, permanecendo apenas como o quadro de pilha atual, por exemplo. Por outro lado, uma referência, conforme representado por um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) interface permanece como o valor permanece na memória.  
  
 O IDE pode usar o `IDebugProperty2` interface para permitir aos usuários navegar e modificar propriedades em tempo de execução.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)