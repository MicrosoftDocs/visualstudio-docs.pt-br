---
title: IDebugCanStopEvent2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 48f049648fcbd93d7ad7411a4dfeba8bbdb4431d
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31105600"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
Essa interface é usada para solicitar que o Gerenciador de sessão de depuração (SDM) se é preciso parar no local atual do código.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCanStopEvent2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface para oferecer suporte a percorrer o código-fonte. O [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) interface deve ser implementada no mesmo objeto dessa interface (usa o SDM [QueryInterface](/cpp/atl/queryinterface) para acessar o `IDebugEvent2` interface).  
  
 A implementação desta interface deve se comunicar a chamada do SDM de [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) para o mecanismo de depuração. Por exemplo, isso pode ser feito com uma mensagem postada a manipulação de mensagens do mecanismo de depuração thread ou o objeto que implementa essa interface pode manter uma referência para o mecanismo de depuração e retorno de chamada para o mecanismo de depuração com o sinalizador passado para `IDebugCanStopEvent2::CanStop`.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O DE pode enviar esse método sempre que o DE é solicitado a continuar a execução e o DE é percorrer o código. Esse evento é enviado usando o [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) função de retorno de chamada fornecida pelo SDM quando anexado ao programa que está sendo depurado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugCanStopEvent2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|Obtém o motivo para esse evento.|  
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|Especifica se o programa que está sendo depurado deve parar no local do evento (e enviar um evento que descreve o motivo para interrupção) ou continuar a execução.|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|Obtém o contexto de documento que descreve o local desse evento.|  
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|Obtém o contexto de código que descreve o local desse evento.|  
  
## <a name="remarks"></a>Comentários  
 O DE envia essa interface se as etapas de usuário em uma função e DE não encontrar nenhuma informação de depuração ou as informações de depuração existem, mas a DE não sabe se o código-fonte pode ser exibido para esse local.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)