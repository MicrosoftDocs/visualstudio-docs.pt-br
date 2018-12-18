---
title: IDebugApplication::HandleBreakPoint | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleBreakPoint
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleBreakPoint
ms.assetid: 97219bdf-a39a-4e69-81ac-4ca2afe77ce5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 16b05533c566cb90529766d81fb7197dbc284664
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726136"
---
# <a name="idebugapplicationhandlebreakpoint"></a>IDebugApplication::HandleBreakPoint
Faz com que o thread atual bloquear e envia uma notificação do ponto de interrupção ao depurador do IDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT HandleBreakPoint(  
   BREAKREASON         br,  
   BREAKRESUMEACTION*  pbra  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `br`  
 [in] O motivo para a interrupção.  
  
 `pbra`  
 [out] Ação a ser tomada quando o depurador retoma o aplicativo.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Um mecanismo de linguagem chama esse método no contexto de um thread que atinge um ponto de interrupção. Esse método bloqueia o thread atual e envia uma notificação de ponto de interrupção ao depurador do IDE. Quando o depurador retoma o aplicativo, o `pbra` parâmetro especifica a ação a tomar.  
  
> [!NOTE]
>  O mecanismo de linguagem pode ser chamado pelo thread de realizar tarefas como enumerar pilha quadros ou avaliar expressões durante o ponto de interrupção.  
  
 Este método faz com que `IApplicationDebugger::onHandleBreakPoint` seja chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugApplication](../../winscript/reference/idebugapplication-interface.md)   
 [IApplicationDebugger::onHandleBreakPoint](../../winscript/reference/iapplicationdebugger-onhandlebreakpoint.md)   
 [Enumeração BREAKREASON](../../winscript/reference/breakreason-enumeration.md)   
 [BREAKRESUMEACTION Enumeration](../../winscript/reference/breakresumeaction-enumeration.md)