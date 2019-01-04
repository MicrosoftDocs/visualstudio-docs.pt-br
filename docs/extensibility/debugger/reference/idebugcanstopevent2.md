---
title: IDebugCanStopEvent2 | Microsoft Docs
ms.date: 11/04/2016
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
ms.openlocfilehash: c5313595bd96b2176255822425d11776eedaedbe
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53942236"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
Essa interface é usada para o Gerenciador de sessão de depuração (SDM) de perguntar se deseja interromper no local atual do código.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCanStopEvent2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DES) implementa essa interface para dar suporte a percorrer o código-fonte. O [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) interface deve ser implementada no mesmo objeto como essa interface (usa o SDM [QueryInterface](/cpp/atl/queryinterface) para acessar o `IDebugEvent2` interface).  
  
 A implementação dessa interface deve se comunicar a chamada do SDM [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) para o mecanismo de depuração. Por exemplo, isso pode ser feito com uma mensagem publicada em um thread de manipulação de mensagens do mecanismo de depuração ou o objeto que implementa essa interface pode conter uma referência para o mecanismo de depuração e retornou a chamada para o mecanismo de depuração com o sinalizador passado para `IDebugCanStopEvent2::CanStop`.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O DE pode enviar esse método sempre que o DE é solicitado a continuar a execução e o DE está percorrendo o código. Esse evento é enviado usando o [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) função de retorno de chamada fornecida pelo SDM quando anexado a programa que está sendo depurado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugCanStopEvent2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|Obtém o motivo para esse evento.|  
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|Especifica se o programa que está sendo depurado deve parar no local do evento (e enviar um evento que descreve o motivo para interrupção) ou simplesmente continuar a execução.|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|Obtém o contexto do documento que descreve o local desse evento.|  
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|Obtém o contexto de código que descreve o local desse evento.|  
  
## <a name="remarks"></a>Comentários  
 O DE envia essa interface se as etapas de usuário em uma função e o DE não encontrar nenhuma informação de depuração ou informações de depuração existem, mas a DE não sabe se o código-fonte pode ser exibido para esse local.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)