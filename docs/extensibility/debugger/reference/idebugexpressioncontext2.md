---
title: IDebugExpressionContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89919ca38c534a292da3e803e823c97a618d534b
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54927431"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
Essa interface representa um contexto de avaliação de expressão  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugExpressionContext2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DES) implementa essa interface para representar um contexto no qual uma expressão pode ser avaliada.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Uma chamada para [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) retorna essa interface. Essa interface é acessível somente quando o programa que está sendo depurado foi pausado e um quadro de pilha está disponível.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugExpressionContext2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|Recupera o nome do contexto de avaliação.|  
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|Analisa uma expressão com base em texto para avaliação.|  
  
## <a name="remarks"></a>Comentários  
 Um contexto de avaliação pode ser pensado como um escopo para a execução de avaliação da expressão.  
  
 Quando um programa foi interrompida, o Gerenciador de sessão de depuração (SDM) obtém um quadro de pilha de com uma chamada para [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md). Em seguida, chama o SDM [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter o `IDebugExpressionContext2` interface. Isso é seguido por uma chamada para [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para criar um [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) interface, que representa a expressão analisada pronta para ser avaliada.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)   
 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)