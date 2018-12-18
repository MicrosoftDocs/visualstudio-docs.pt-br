---
title: IDebugEventCallback2 | Microsoft Docs
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
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2c1e0f6425b6c466d54b6ed24bace0e406e7035d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792093"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface é usada pelo mecanismo de depuração (DE) para enviar eventos de depuração para o Gerenciador de sessão de depuração (SDM).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEventCallback2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] implementa essa interface para receber eventos de um mecanismo de depuração.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Um mecanismo de depuração normalmente recebe essa interface quando chama o SDM [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md), [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md), ou [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md). Um mecanismo de depuração para enviar eventos para o SDM chamando [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugEventCallback2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|Envia notificação de eventos para o SDM de depuração.|  
  
## <a name="remarks"></a>Comentários  
 Embora [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) e [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) Especifica que eles têm um `IDebugEventCallback2` interface, isso não for o caso, e o ponteiro de interface sempre será um valor nulo. Em vez disso, o mecanismo de depuração deve usar o `IDebugEventCallback2` recebidos na chamada à interface [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md), [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md), ou [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md).  
  
 Se um pacote implementa [IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md) no código gerenciado, é altamente recomendável que <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> ser invocada em várias interfaces que são passadas para [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)

