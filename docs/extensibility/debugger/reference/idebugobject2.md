---
title: IDebugObject2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d5e60c9e084872b08ec8d38b784b47969af2d52e
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31118915"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
>  No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão do CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface fornece informações adicionais sobre um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugObject2 : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O avaliador de expressão implementa essa interface para oferecer suporte a aliases e acesso a informações sobre o objeto.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Um [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) interface pode obter essa interface usando [QueryInterface](/cpp/atl/queryinterface). Além disso, [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) retorna essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos de [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) interface, o `IDebugObject2` interface implementa o seguinte:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|Obtém o campo ou variável (se houver) que pode ser fazendo a propriedade representada pelo objeto.|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|Obtém o objeto de código gerenciado que representa o valor do objeto.|  
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|Cria uma ID exclusiva para esse objeto ou retorna um alias existente.|  
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|Obtém o alias associado com esse objeto, se houver.|  
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|Obtém o tipo do objeto.|  
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|Determina se este objeto representa dados de usuário.|  
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|Determina se o estado de editar e continuar não é mais válido.<br /><br /> O avaliador de expressão personalizada não implementa esse método (sempre deve retornar `E_NOTIMPL`).|  
  
## <a name="remarks"></a>Comentários  
 Consulte [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) para obter mais informações sobre aliases.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)   
 [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)