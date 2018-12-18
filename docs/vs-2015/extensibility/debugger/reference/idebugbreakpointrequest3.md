---
title: IDebugBreakpointRequest3 | Microsoft Docs
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
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2f6e037b4901f7856a286ffdfe999562740217f3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732934"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa as informações necessárias para criar e associar a qualquer tipo de ponto de interrupção. Ele é uma extensão da [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugBreakpointRequest3 : IDebugBreakpointRequest2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O Gerenciador de sessão de depuração (SDM) normalmente implementa essa interface.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O mecanismo de depuração (DES) acessa essa interface chamando [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) na interface IDebugBreakpointRequest2 recebido em uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Além dos métodos herdados de [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md), o `IDebugBreakpointRequest3` interface expõe o método a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|Obtém as informações de solicitação de ponto de interrupção que descreve esta solicitação de ponto de interrupção.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é usada para fornecer informações adicionais para o DE por meio de [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) estrutura. Essas informações adicionais incluem a ID do fornecedor da Alemanha (na forma de um GUID), o nome de um tracepoint e o nome de uma restrição de ponto de interrupção.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)

