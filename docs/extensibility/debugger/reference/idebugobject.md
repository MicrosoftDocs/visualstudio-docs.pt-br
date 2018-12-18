---
title: IDebugObject | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4cff859d2aa4b3a3c88978e077102e045efe1f3b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31120995"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
>  No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão do CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface representa um objeto que cria o associador para encapsular os valores de expressões e símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugObject : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um avaliador de expressão implementa essa interface para representar um objeto.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Esta interface é a classe base para todos os objetos que o avaliador de expressão usa expressões analisado. Ele é retornado por uma chamada para o [associar](../../../extensibility/debugger/reference/idebugbinder-bind.md) método. [QueryInterface](/cpp/atl/queryinterface) obtém as interfaces mais especializadas dessa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugObject`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|Obtém o tamanho do objeto.|  
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|Obtém o valor do objeto consecutivos de bytes.|  
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|Define o valor do objeto de consecutivos de bytes.|  
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|Define o valor de referência do objeto.|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|Obtém o contexto de memória que representa o endereço do valor do objeto.|  
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|Cria uma cópia do objeto gerenciado no espaço de endereço do mecanismo de depuração.|  
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|Testa se este objeto é uma referência nula.|  
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|Compara a um objeto a este.|  
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|Determina se este objeto é somente leitura.|  
|[É proxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|Determina se o objeto é um proxy transparente.|  
  
## <a name="remarks"></a>Comentários  
 O avaliador de expressão usa essa interface como a classe base para representar objetos em uma árvore de análise.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)   
 [Ligação](../../../extensibility/debugger/reference/idebugbinder-bind.md)