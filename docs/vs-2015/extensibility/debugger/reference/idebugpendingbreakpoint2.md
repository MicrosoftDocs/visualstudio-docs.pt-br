---
title: IDebugPendingBreakpoint2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1238fcbce22db3f3bc3e32019aac886c79d0c114
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923145"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa um ponto de interrupção que está pronto para associar a um local de código.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugPendingBreakpoint2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DES) implementa essa interface como parte de seu suporte para pontos de interrupção.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) cria um ponto de interrupção pendente de uma [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) interface. Uma chamada para [vincular](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) cria um `IDebugBreakpoint2` interface que representa um ponto de interrupção associado no programa.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugPendingBreakpoint2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|Determina se este ponto de interrupção pendente pode associar a um local de código.|  
|[Associar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|Associa a esse ponto de interrupção pendente para um ou mais locais de código.|  
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|Obtém o estado deste pendente do ponto de interrupção.|  
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|Obtém a solicitação de ponto de interrupção que foi usada para criar esse ponto de interrupção pendente.|  
|[Virtualizar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|Alterna o estado virtualizado isso pendente do ponto de interrupção.|  
|[Habilitar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|Alterna o estado habilitado isso pendente do ponto de interrupção.|  
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|Define ou altera a condição associada a este pendente do ponto de interrupção.|  
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|Define ou altera a contagem de passagem associada a este pendente do ponto de interrupção.|  
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|Enumera todos os pontos de interrupção limitados do ponto de interrupção pendente.|  
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|Enumera todos os pontos de interrupção de erro que resultaram de ponto de interrupção pendente.|  
|[Excluir](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|Exclui esse ponto de interrupção pendente e todos os pontos de interrupção associados dele.|  
  
## <a name="remarks"></a>Comentários  
 `IDebugPendingBreakpoint2` pode ser pensada como um provedor de todas as informações necessárias para associar um ponto de interrupção para o código que pode ser aplicado a um ou vários programas.  
  
 Um ponto de interrupção pendente pode potencialmente gerar mais de um ponto de interrupção associado. Por exemplo, um ponto de interrupção em um modelo de estilo C++ pôde produzir um ponto de interrupção associado para cada instância exclusiva do modelo.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
