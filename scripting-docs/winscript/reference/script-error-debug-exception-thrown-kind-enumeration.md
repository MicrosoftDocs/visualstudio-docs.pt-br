---
title: Enumeração SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b3aa4966-e110-4b30-b368-1281a9740dbd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6fe5b308ea75956d9e5826b4daadaef3a823141f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734146"
---
# <a name="scripterrordebugexceptionthrownkind-enumeration"></a>Enumeração SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND
Indica o tipo de exceção lançada. Essa enumeração é usada pelo [IActiveScriptErrorDebug110::GetExceptionThrownKind](../../winscript/reference/iactivescripterrordebug110-getexceptionthrownkind.md) método.  
  
> [!IMPORTANT]
>  Essas constantes são implementadas pela versão 11.0 PDM e superiores. Localizado em. activdbg100.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Valor|Descrição|  
|------------|-----------|-----------------|  
|ETK_FIRST_CHANCE|0x00000000|A exceção é uma exceção de primeira tentativa.|  
|ETK_USER_UNHANDLED|0x00000001|A exceção não é manipulada no código de usuário.|  
|ETK_UNHANDLED|0x00000002|A exceção não é manipulada no código.|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptErrorDebug110 Interface](../../winscript/reference/iactivescripterrordebug110-interface.md)