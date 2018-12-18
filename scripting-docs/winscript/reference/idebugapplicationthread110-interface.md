---
title: Interface IDebugApplicationThread110 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread110 Interface
ms.assetid: 25bc351f-3451-4387-9302-078f6292ddff
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aee30ae68319810f58bf31f8d0eb32cf8f30d34c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726346"
---
# <a name="idebugapplicationthread110-interface"></a>Interface IDebugApplicationThread110
Fornece a funcionalidade mais para o [IDebugApplicationThread Interface](../../winscript/reference/idebugapplicationthread-interface.md) interface.  
  
> [!IMPORTANT]
>  Esta interface é implementada pelo PDM v11.0 e superiores. Localizado em. activdbg100.h.  
  
## <a name="methods"></a>Métodos  
 A interface `IDebugApplicationThread110` expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugApplicationThread110::AsynchronousCallIntoThread](../../winscript/reference/idebugapplicationthread110-asynchronouscallintothread.md)|Faz uma chamada assíncrona no thread principal.|  
|[IDebugApplicationThread110::GetActiveThreadRequestCount](../../winscript/reference/idebugapplicationthread110-getactivethreadrequestcount.md)|Uma contagem de quantas solicitações do thread de thread do PDM alternância de mecanismos de processamento no momento. Normalmente, 0 ou 1, mas ele 's possíveis para isso será maior se uma chamada do thread inicia o processamento, mas dispara uma chamada síncrona fora do thread ou caso contrário, suspende o thread (por exemplo, Disparando um evento IDebugApplicationEvents emitida no depurador thread)|  
|[IDebugApplicationThread110::IsSuspendedForBreakPoint](../../winscript/reference/idebugapplicationthread110-issuspendedforbreakpoint.md)|[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md) foi chamado neste thread e ainda não foi concluído.|  
|[IDebugApplicationThread110::IsThreadCallable](../../winscript/reference/idebugapplicationthread110-isthreadcallable.md)|Esse thread está em um estado que pode processar chamadas feitas usando o thread do PDM alternância mecanismos (como SynchronousCallInThread).|