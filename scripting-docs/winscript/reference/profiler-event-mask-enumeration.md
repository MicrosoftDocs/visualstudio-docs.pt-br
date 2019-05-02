---
title: Enumeração PROFILER_EVENT_MASK | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PROFILER_EVENT_MASK
apilocation:
- scrobj.dll
ms.assetid: c2168408-f4f6-4600-971d-f15b4edf4ca2
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f7230e65e5559d53e56cf6424a34dd44aa4edda7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831636"
---
# <a name="profilereventmask-enumeration"></a>Enumeração PROFILER_EVENT_MASK
Indica os tipos de eventos que devem ser analisados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef enum {  
    PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL = 0x00000001,  
    PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL = 0x00000002,  
    PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL    = 0x00000004,  
    PROFILER_EVENT_MASK_TRACE_ALL =  
    PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL |  
    PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL,  
    PROFILER_EVENT_MASK_TRACE_ALL_WITH_DOM = PROFILER_EVENT_MASK_TRACE_ALL |  
    PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL  
} PROFILER_EVENT_MASK;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|PROFILER_EVENT_MASK_TRACE_SCRIPT_FUNCTION_CALL|Funções de perfis que são definidas no script escrito pelo usuário e código dinâmico.|  
|PROFILER_EVENT_MASK_TRACE_NATIVE_FUNCTION_CALL|Funções nativas perfis definidos pelo mecanismo de script.|  
|PROFILER_EVENT_MASK_TRACE_ALL|Perfis de todas as funções de mecanismo de script e definidas pelo usuário, excluindo chamadas no modelo de objeto de documento (DOM).|  
|PROFILER_EVENT_MASK_TRACE_DOM_FUNCTION_CALL|Funções de perfis que chamam o DOM.|  
|PROFILER_EVENT_MASK_TRACE_ALL_WITH_DOM|Perfis de todas as funções, incluindo as chamadas no DOM.|  
  
## <a name="see-also"></a>Consulte também  
 [Script ativo Profiler constantes, enumerações e estruturas](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)   
 [IActiveScriptProfilerControl::SetProfilerEventMask](../../winscript/reference/iactivescriptprofilercontrol-setprofilereventmask.md)   
 [IActiveScriptProfilerControl::StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)