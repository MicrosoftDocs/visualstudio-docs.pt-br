---
title: IDebugObject | Microsoft Docs
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
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 67db4808b8f20ea759ad5847508307e9efff5620
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51785671"
---
# <a name="idebugobject"></a>IDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface representa um objeto que o associador cria para encapsular os valores de símbolos e expressões.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugObject : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um avaliador de expressão implementa essa interface para representar um objeto.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é a classe base para todos os objetos que o avaliador de expressão usa expressões analisado. Ele é retornado por uma chamada para o [associar](../../../extensibility/debugger/reference/idebugbinder-bind.md) método. [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) obtém as interfaces mais especializadas dessa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugObject`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|Obtém o tamanho do objeto.|  
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|Obtém o valor do objeto consecutivos de bytes.|  
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|Define o valor do objeto de uma série consecutiva de bytes.|  
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|Define o valor de referência do objeto.|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|Obtém o contexto de memória que representa o endereço do valor do objeto.|  
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|Cria uma cópia do objeto gerenciado no espaço de endereço do mecanismo de depuração.|  
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|Testa se este objeto é uma referência nula.|  
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|Compara um objeto para esse outro.|  
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|Determina se este objeto é somente leitura.|  
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|Determina se o objeto for um proxy transparente.|  
  
## <a name="remarks"></a>Comentários  
 O avaliador de expressão usa essa interface como a classe base para representar objetos em uma árvore de análise.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)   
 [Associar](../../../extensibility/debugger/reference/idebugbinder-bind.md)

