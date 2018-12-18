---
title: Constantes SCRIPTTHREADID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTTHREADID
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTTHREADID
ms.assetid: 1df9940c-ad0c-42d8-96b9-6a6abe2382e6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc692716115ea0c205b1cfd982b189fffd54a9ac
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734186"
---
# <a name="scriptthreadid-constants"></a>Constantes SCRIPTTHREADID
Usado para especificar o tipo de segmento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef DWORD SCRIPTTHREADID;  
```  
  
## <a name="constants"></a>Constantes  
  
|Constante|Valor|Significado|  
|--------------|-----------|-------------|  
|SCRIPTTHREADID_CURRENT|0xFFFFFFFD|O thread em execução no momento.|  
|SCRIPTTHREADID_BASE|0xFFFFFFFE|O thread de base; ou seja, o thread em que o script do mecanismo foi instanciado.|  
|SCRIPTTHREADID_ALL|0xFFFFFFFF|Todos os threads.|  
  
## <a name="remarks"></a>Comentários  
 O `SCRIPTTHREADID` tipo é usado por `IActiveScript::GetCurrentScriptThreadID`, `IActiveScript::GetScriptThreadID`, `IActiveScript::GetScriptThreadState`, e `IActiveScript::InterruptScriptThread`, mas as constantes só podem ser usadas por `IActiveScript::GetScriptThreadState` e `IActiveScript::InterruptScriptThread`.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)   
 [IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)   
 [IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)