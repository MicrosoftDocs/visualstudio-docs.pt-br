---
title: Interface IRemoteDebugApplicationEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplicationEx Interface
ms.assetid: 8e16164d-dbb2-4488-9507-25ae34f343dc
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3360cea0d1649348a795356ad827b32b6f8ebc19
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729396"
---
# <a name="iremotedebugapplicationex-interface"></a>Interface IRemoteDebugApplicationEx
Representa um aplicativo em execução. Ele não precisa corresponder a um processo do sistema operacional. Normalmente, um depurador tem como alvo um aplicativo para depuração. Normalmente, o Gerenciador de depuração do processo implementa o objeto de aplicativo.  
  
 Além dos métodos herdados de `IUnknown`, o `IRemoteDebugApplicationEx` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IRemoteDebugApplicationEx:GetHostPid](../../winscript/reference/iremotedebugapplicationex-gethostpid.md)|Retorna a ID de processo para o aplicativo host.|  
|GetHostMachineName|Retorna o nome do computador que o aplicativo de host está em execução no.|  
|[IRemoteDebugApplicationEx:SetLocale](../../winscript/reference/iremotedebugapplicationex-setlocale.md)|Define o idioma para a localização do depurador.|  
|[IRemoteDebugApplicationEx:ForceStepMode](../../winscript/reference/iremotedebugapplicationex-forcestepmode.md)|Força o depurador em modo de única etapa.|  
|[IRemoteDebugApplicationEx:RevokeBreak](../../winscript/reference/iremotedebugapplicationex-revokebreak.md)|Revoga um comando de interrupção.|  
|SetProxyBlanketAndAddRef|Atualiza as informações de segurança COM um proxy para um objeto do depurador para garantir a compatibilidade com a depuração remota de sistemas operacionais baseados no Windows 95.|  
|ReleaseFromSetProxyBlanket|Versões AddRef de SetProxyBlanketAndAddRef.|