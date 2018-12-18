---
title: Interface IDebugApplicationThreadEvents110 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThreadEvents110 Interface
ms.assetid: 91a98b0e-7c81-4118-af75-82f75fd4f25a
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6aaf312b1730696b812172aeea175619e911d03a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726266"
---
# <a name="idebugapplicationthreadevents110-interface"></a>Interface IDebugApplicationThreadEvents110
Adiciona mais eventos do thread. Esses eventos são apenas locais. Ou seja, você pode assiná-los apenas no processo que está sendo depurado, usando o [IConnectionPoint](http://go.microsoft.com/fwlink/?LinkId=232738) de aviso e unadvise métodos em objetos de thread de aplicativo PDM (os objetos que implementam [IDebugApplicationThread Interface](../../winscript/reference/idebugapplicationthread-interface.md)). Eles ocorrem no thread em que eles são provenientes.  
  
> [!IMPORTANT]
>  Esta interface é implementada pelo PDM v11.0 e superiores. Localizado em. activdbg100.h.  
  
## <a name="methods"></a>Métodos  
 A interface `IDebugActivationThreadEvents110` expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugApplicationThreadEvents110 ::OnBeginThreadRequest](../../winscript/reference/idebugapplicationthreadevents110-onbeginthreadrequest.md)|Uma chamada o thread usando o thread do PDM alternância foi iniciado.|  
|[IDebugApplicationThreadEvents110::OnResumeFromBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onresumefrombreakpoint.md)|O thread está voltando a partir de um ponto de interrupção e ficará ativo novamente.|  
|[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md)|O thread está sendo suspenso para um ponto de interrupção e pode lidar com chamadas que exigem o thread totalmente ser suspenso.|  
|[IDebugApplicationThreadEvents110::OnThreadRequestComplete](../../winscript/reference/idebugapplicationthreadevents110-onthreadrequestcomplete.md)|Uma chamada para o thread usando o thread do PDM alternância foi concluída.|