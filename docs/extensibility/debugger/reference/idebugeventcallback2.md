---
title: IDebugEventCallback2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 68d29d928f310cb045ed712a151f9275446465a4
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31116198"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
Essa interface é usada pelo mecanismo de depuração (DE) para enviar eventos de depuração para o Gerenciador de sessão de depuração (SDM).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEventCallback2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] implementa essa interface para receber eventos de um mecanismo de depuração.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Um mecanismo de depuração costuma recebe esta interface quando chama o SDM [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md), [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md), ou [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md). Um mecanismo de depuração envia eventos para o SDM chamando [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugEventCallback2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|Envia notificação de eventos para o SDM de depuração.|  
  
## <a name="remarks"></a>Comentários  
 Embora [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) e [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) Especifica que eles têm um `IDebugEventCallback2` interface, isso não for o caso, e o ponteiro de interface sempre será um valor nulo. Em vez disso, o mecanismo de depuração deve usar o `IDebugEventCallback2` interface recebida na chamada para [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md), [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md), ou [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md).  
  
 Se um pacote implementa [IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md) em código gerenciado, é altamente recomendável que <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> ser chamada em várias interfaces que são passadas para [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)