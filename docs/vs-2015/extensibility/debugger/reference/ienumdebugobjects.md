---
title: IEnumDebugObjects | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c6956135476798445fed8352e8d6ca0677949a36
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929710"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Essa interface representa uma coleção de objetos que implementam o [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) interface.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugObjects : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O avaliador de expressão implementa essa interface para fornecer conjuntos de objetos que implementam o [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) interface. Observe que isso não é uma enumeração COM padrão devido à presença do [GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md) método.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md) retorna essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Essa interface implementa os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|Recupera o próximo conjunto de [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objetos da enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|Ignora um número especificado de entradas.|  
|[Reiniciar](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|Redefine a enumeração para a primeira entrada.|  
|[Clonar](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|Recupera uma cópia da enumeração atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|Recupera o número de entradas na enumeração.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface permite que um mecanismo de depuração enumerar sobre um conjunto de objetos em uma matriz.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
