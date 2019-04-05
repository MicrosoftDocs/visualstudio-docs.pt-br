---
title: IDebugBreakpointRequest2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 263b947fff45eafd2d2e5afc029572b69ea24b82
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58924544"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa as informações necessárias para criar e associar a qualquer tipo de ponto de interrupção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugBreakpointRequest2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O Gerenciador de sessão de depuração (SDM) normalmente implementa essa interface.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O mecanismo de depuração (DES) recebe essa interface por meio de uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) para criar um ponto de interrupção pendente. Uma chamada para [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) pode recuperar essa interface de.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugBreakpointRequest2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|Obtém o tipo de local de ponto de interrupção dessa solicitação de ponto de interrupção.|  
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|Obtém as informações de solicitação de ponto de interrupção que descreve esta solicitação de ponto de interrupção.|  
  
## <a name="remarks"></a>Comentários  
 Após o programa que está sendo depurado foi carregado, uma chamada para [associar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) associa um ponto de interrupção pendente para o local solicitado no programa.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)   
 [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)   
 [Associar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
