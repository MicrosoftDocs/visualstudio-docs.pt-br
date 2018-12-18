---
title: Enumeração PROFILER_SCRIPT_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PROFILER_SCRIPT_TYPE
apilocation:
- scrobj.dll
ms.assetid: 3ab6633a-6241-44f0-b837-14336f70c71e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 279969ec0b50f705e39d2e29e700adc1e833ead3
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734116"
---
# <a name="profilerscripttype-enumeration"></a>Enumeração PROFILER_SCRIPT_TYPE
Especifica o tipo de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum {  
    PROFILER_SCRIPT_TYPE_USER,  
    PROFILER_SCRIPT_TYPE_DYNAMIC,  
    PROFILER_SCRIPT_TYPE_NATIVE,  
    PROFILER_SCRIPT_TYPE_DOM  
} PROFILER_SCRIPT_TYPE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|PROFILER_SCRIPT_TYPE_USER|Especifica o código de script gravados pelo usuário.|  
|PROFILER_SCRIPT_TYPE_DYNAMIC|Especifica o código de script que é gerado dinamicamente durante a execução.|  
|PROFILER_SCRIPT_TYPE_NATIVE|Especifica o tipo de script para funções nativas e objetos que são definidos pelo mecanismo de script.|  
|PROFILER_SCRIPT_TYPE_DOM|Especifica uma chamada para o modelo DOM (Document Object) do Internet Explorer, por exemplo, uma chamada para o `document.getElementById` método.|  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas, enumerações e constantes do criador de perfil de Script ativo](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)   
 [IActiveScriptProfilerCallback::ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)   
 [IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)   
 [IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)