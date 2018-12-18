---
title: Interface IRemoteDebugApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication interface
ms.assetid: 96bf2a3f-049f-46ba-86ad-57fc184343a2
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea91afdc44b70a91846d7b1a3dc4c017c0c4c80e
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729596"
---
# <a name="iremotedebugapplication-interface"></a>Interface IRemoteDebugApplication
Representa um aplicativo em execução. Ele não precisa corresponder a um processo do sistema operacional. Normalmente, um depurador tem como alvo um aplicativo para depuração. Normalmente, o Gerenciador de depuração do processo implementa o objeto de aplicativo.  
  
 Além dos métodos herdados de `IUnknown`, o `IRemoteDebugApplication` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IRemoteDebugApplication::ResumeFromBreakPoint](../../winscript/reference/iremotedebugapplication-resumefrombreakpoint.md)|Continua um aplicativo que está atualmente em um ponto de interrupção.|  
|[IRemoteDebugApplication::CauseBreak](../../winscript/reference/iremotedebugapplication-causebreak.md)|Faz com que o aplicativo para invadir o depurador o mais breve possível.|  
|[IRemoteDebugApplication::ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)|Conecta-se um depurador para este aplicativo.|  
|[IRemoteDebugApplication::DisconnectDebugger](../../winscript/reference/iremotedebugapplication-disconnectdebugger.md)|Desconecta o depurador atual do aplicativo.|  
|[IRemoteDebugApplication::GetDebugger](../../winscript/reference/iremotedebugapplication-getdebugger.md)|Retorna o depurador atual conectado ao aplicativo.|  
|[IRemoteDebugApplication::CreateInstanceAtApplication](../../winscript/reference/iremotedebugapplication-createinstanceatapplication.md)|Fornece um mecanismo para o depurador IDE, em execução fora do processo para o aplicativo para criar objetos no processo do aplicativo.|  
|[IRemoteDebugApplication::QueryAlive](../../winscript/reference/iremotedebugapplication-queryalive.md)|Indica se o aplicativo está respondendo.|  
|[IRemoteDebugApplication::EnumThreads](../../winscript/reference/iremotedebugapplication-enumthreads.md)|Enumera todos os threads conhecidos para ser associado ao aplicativo.|  
|[IRemoteDebugApplication::GetName](../../winscript/reference/iremotedebugapplication-getname.md)|Retorna o nome deste nó de aplicativo.|  
|[IRemoteDebugApplication::GetRootNode](../../winscript/reference/iremotedebugapplication-getrootnode.md)|Retorna o nó de aplicativo em que todos os nós associados ao aplicativo são adicionados.|  
|[IRemoteDebugApplication::EnumGlobalExpressionContexts](../../winscript/reference/iremotedebugapplication-enumglobalexpressioncontexts.md)|Enumera os contextos de expressão global para todos os idiomas em execução neste aplicativo.|