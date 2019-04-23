---
title: IDebugFunctionObject2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ba0ec3092943c0e0cb5593f020926c705cc0eb0a
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60037953"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Representa uma função e aprimora a [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) interface.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugFunctionObject2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um avaliador de expressão (EE) implementa essa interface para representar uma função.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Métodos dessa interface adiar aqueles **IDebugFunctionObject** das seguintes maneiras:  
  
- O **IDebugEvaluate** método usa sinalizadores.  
  
- O **CreateObject** método usa um tempo limite e sinalizadores.  
  
- O **CreateStringObjectWithLength** método usa um comprimento.  
  
## <a name="methods"></a>Métodos  
 Essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|Cria um objeto que usa um construtor que recebe as configurações de sinalizador de avaliação e um valor de tempo limite.|  
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|Cria um objeto de cadeia de caracteres que tem o comprimento especificado.|  
|[Avaliar](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|Chama a função e retorna o valor resultante como um objeto.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: EE.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
