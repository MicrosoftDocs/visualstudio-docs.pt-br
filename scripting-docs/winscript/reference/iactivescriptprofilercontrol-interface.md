---
title: Interface IActiveScriptProfilerControl | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1448b394-9743-41b5-8eb9-5026a45773a4
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0d598302ae78ca0b2a1e7c1f94c949800378a2e
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724666"
---
# <a name="iactivescriptprofilercontrol-interface"></a>Interface IActiveScriptProfilerControl
Implementado pelo mecanismo de script que dá suporte à criação de perfil. Normalmente, um objeto que implementa o `IActiveScriptProfilerControl` também implementa o [IActiveScript](../../winscript/reference/iactivescript.md) interface. Nesse caso, você pode obter um identificador para o `IActiveScriptProfilerControl` interface chamando o `IUnknown::QueryInterface` método no objeto. A interface fornece os métodos necessários para parar e iniciar a criação de perfil no mecanismo de script.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptProfilerControl::StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)|Inicia a criação de perfil no mecanismo de script.|  
|[IActiveScriptProfilerControl::SetProfilerEventMask](../../winscript/reference/iactivescriptprofilercontrol-setprofilereventmask.md)|Define o criador de perfil máscara de evento no mecanismo de script.|  
|[IActiveScriptProfilerControl::StopProfiling](../../winscript/reference/iactivescriptprofilercontrol-stopprofiling.md)|Interrompe a criação de perfil no mecanismo de script.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces do criador de perfil de script ativo](../../winscript/reference/active-script-profiler-interfaces.md)