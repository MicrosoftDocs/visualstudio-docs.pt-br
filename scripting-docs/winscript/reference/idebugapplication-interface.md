---
title: Interface IDebugApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication interface
ms.assetid: 5dfa941b-4cd9-46fa-a230-3f41df9ea205
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 07964292785634212099a0bfcf8174ebb55e8713
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727436"
---
# <a name="idebugapplication-interface"></a>Interface IDebugApplication
Expõe métodos de depuração remota não para uso por hosts e mecanismos de idioma.  
  
 Além dos métodos herdados de `IRemoteDebugApplication`, o `IDebugApplication` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugApplication::SetName](../../winscript/reference/idebugapplication-setname.md)|Define o nome do aplicativo.|  
|[IDebugApplication::StepOutComplete](../../winscript/reference/idebugapplication-stepoutcomplete.md)|Notifica o Gerenciador de depuração do processo que um mecanismo de linguagem no modo de única etapa está prestes a retornar ao chamador.|  
|[IDebugApplication::DebugOutput](../../winscript/reference/idebugapplication-debugoutput.md)|Faz com que a cadeia de caracteres específica a ser exibida pelo depurador IDE.|  
|[IDebugApplication::StartDebugSession](../../winscript/reference/idebugapplication-startdebugsession.md)|Inicia o depurador padrão do IDE e anexa uma sessão de depuração para este aplicativo, se uma já não está anexada.|  
|[IDebugApplication::HandleBreakPoint](../../winscript/reference/idebugapplication-handlebreakpoint.md)|Faz com que o thread atual bloquear e envia uma notificação do ponto de interrupção ao depurador do IDE.|  
|[IDebugApplication::Close](../../winscript/reference/idebugapplication-close.md)|Faz com que esse aplicativo para liberar todas as referências e insira um estado inativo.|  
|[IDebugApplication::GetBreakFlags](../../winscript/reference/idebugapplication-getbreakflags.md)|Retorna os sinalizadores de quebra atual para o aplicativo.|  
|[IDebugApplication::GetCurrentThread](../../winscript/reference/idebugapplication-getcurrentthread.md)|Retorna o thread associado com o thread em execução no momento.|  
|[IDebugApplication::CreateAsyncDebugOperation](../../winscript/reference/idebugapplication-createasyncdebugoperation.md)|Fornece acesso assíncrono a uma operação de depuração síncrona determinado.|  
|[IDebugApplication::AddStackFrameSniffer](../../winscript/reference/idebugapplication-addstackframesniffer.md)|Adiciona um provedor de enumerador de quadro de pilha para este aplicativo.|  
|[IDebugApplication::RemoveStackFrameSniffer](../../winscript/reference/idebugapplication-removestackframesniffer.md)|Remove um provedor de enumerador de quadro de pilha desse aplicativo.|  
|[IDebugApplication::QueryCurrentThreadIsDebuggerThread](../../winscript/reference/idebugapplication-querycurrentthreadisdebuggerthread.md)|Determina se o thread de execução atual é o thread do depurador.|  
|[IDebugApplication::SynchronousCallInDebuggerThread](../../winscript/reference/idebugapplication-synchronouscallindebuggerthread.md)|Fornece um mecanismo para o chamador executar o código no thread do depurador.|  
|[IDebugApplication::CreateApplicationNode](../../winscript/reference/idebugapplication-createapplicationnode.md)|Cria um novo nó de aplicativo que está associado um provedor de documento específico.|  
|[IDebugApplication::FireDebuggerEvent](../../winscript/reference/idebugapplication-firedebuggerevent.md)|Dispara um evento genérico para o depurador `IApplicationDebugger` interface.|  
|[IDebugApplication::HandleRuntimeError](../../winscript/reference/idebugapplication-handleruntimeerror.md)|Faz com que o thread atual bloquear e envia uma notificação de erro para o depurador do IDE.|  
|[IDebugApplication::FCanJitDebug](../../winscript/reference/idebugapplication-fcanjitdebug.md)|Determina se um depurador do just-in-time (JIT) está registrado.|  
|[IDebugApplication::FIsAutoJitDebugEnabled](../../winscript/reference/idebugapplication-fisautojitdebugenabled.md)|Determina se um depurador JIT está registrado para hosts sem depuração automática.|  
|[IDebugApplication::AddGlobalExpressionContextProvider](../../winscript/reference/idebugapplication-addglobalexpressioncontextprovider.md)|Adiciona um provedor de contexto de expressão global para este aplicativo.|  
|[IDebugApplication::RemoveGlobalExpressionContextProvider](../../winscript/reference/idebugapplication-removeglobalexpressioncontextprovider.md)|Remove um provedor de contexto de expressão global desse aplicativo.|