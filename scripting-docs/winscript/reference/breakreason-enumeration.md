---
title: Enumeração BREAKREASON | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- BREAKREASON
apilocation:
- scrobj.dll
helpviewer_keywords:
- BREAKREASON enumeration
ms.assetid: bde07ede-2f9b-4fa2-affc-f9405683f5f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6f656bdf4e3bc85a014ff8d3011708799aa44bcd
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572626"
---
# <a name="breakreason-enumeration"></a>Enumeração BREAKREASON
Indica o que causou a interrupção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef enum tagBREAKREASON {  
   BREAKREASON_STEP,  
   BREAKREASON_BREAKPOINT,  
   BREAKREASON_DEBUGGER_BLOCK,  
   BREAKREASON_HOST_INITIATED,  
   BREAKREASON_LANGUAGE_INITIATED,  
   BREAKREASON_DEBUGGER_HALT,  
   BREAKREASON_ERROR,  
   BREAKREASON_JIT  
} BREAKREASON;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|BREAKREASON_STEP|O mecanismo de idioma está no modo de depuração.|  
|BREAKREASON_BREAKPOINT|O mecanismo de linguagem encontrou um ponto de interrupção explícito.|  
|BREAKREASON_DEBUGGER_BLOCK|O mecanismo de linguagem encontrou um bloco de depurador em outro thread.|  
|BREAKREASON_HOST_INITIATED|O host solicitou uma interrupção.|  
|BREAKREASON_LANGUAGE_INITIATED|O mecanismo de idioma solicitou uma interrupção.|  
|BREAKREASON_DEBUGGER_HALT|O IDE do depurador solicitou uma interrupção.|  
|BREAKREASON_ERROR|Um erro de execução causou a interrupção.|  
|BREAKREASON_JIT|Causado pela inicialização da depuração JIT.|  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)