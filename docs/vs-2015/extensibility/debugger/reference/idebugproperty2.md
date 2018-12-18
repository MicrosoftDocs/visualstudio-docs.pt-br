---
title: IDebugProperty2 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cc5e780bb5e211b8900a22b181749e0376c6f242
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742613"
---
# <a name="idebugproperty2"></a>IDebugProperty2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa uma propriedade de quadro de pilha, uma propriedade de documento do programa ou outra propriedade. A propriedade é geralmente o resultado de uma avaliação de expressão.  
  
> [!NOTE]
>  Esse uso de "property" não deve ser confundido com esse que significa que uma variável de membro de uma classe, embora um `IDebugProperty2` pode representar essa entidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProperty2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O DE implementa essa interface para representar um determinado tipo de valor. Por exemplo, o valor pode ser um valor numérico como resultado de uma avaliação de expressão, um contexto de memória usado para exibir a memória ou uma lista de registros e seus valores.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chame [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter essa interface, que representa o resultado de uma avaliação. `IDebugExpression2::EvaluateAsync` retorna essa interface, enviando uma [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) interface para o SDM, que por sua vez chama [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) ao recuperar a propriedade.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) retorna essa interface para fornecer o documento de script associado.  
  
 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) retorna essa interface para representar o valor de retorno de uma função.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) retorna essa interface para representar várias propriedades do programa como um nome ou um contexto de memória.  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) retorna essa interface para representar várias propriedades do quadro de pilha, como variáveis locais.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugProperty2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|Preenche um [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estrutura que descreve uma propriedade.|  
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|Define o valor de uma propriedade de uma cadeia de caracteres.|  
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|Define o valor da propriedade do valor de uma determinada referência.|  
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|Enumera os filhos de uma propriedade.|  
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|Retorna o pai de uma propriedade.|  
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|Retorna a propriedade que descreve a propriedade mais derivado de uma propriedade.|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|Retorna os bytes de memória que compõem o valor de uma propriedade.|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|Retorna o contexto de memória para um valor da propriedade.|  
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|Retorna o tamanho, em bytes, do valor da propriedade.|  
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|Retorna uma referência ao valor desta propriedade.|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|Retorna as informações estendidas de uma propriedade.|  
  
## <a name="remarks"></a>Comentários  
 Uma propriedade, conforme representado por um `IDebugProperty2` interface, pode ser pensada como um valor com um nome, um tipo e um endereço. Em termos mais gerais, um `IDebugProperty2` pode representar qualquer coisa que tem uma estrutura hierárquica, com os pais e nós filho.  
  
 Uma propriedade é normalmente transitório, permanecendo apenas como o quadro de pilha atual, por exemplo. Por outro lado, uma referência, conforme representado por um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) interface dura desde que o valor permanece na memória.  
  
 O IDE pode usar o `IDebugProperty2` interface para permitir aos usuários navegar e modificar propriedades em tempo de execução.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

