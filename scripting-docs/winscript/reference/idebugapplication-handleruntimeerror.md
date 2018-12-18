---
title: IDebugApplication::HandleRuntimeError | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleRuntimeError
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleRuntimeError
ms.assetid: f8f3bbaf-09e5-4d01-8a35-f380bc7ff8ed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eead4780ff061ff9c7280aeee0936c8f64741981
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725786"
---
# <a name="idebugapplicationhandleruntimeerror"></a>IDebugApplication::HandleRuntimeError
Faz com que o thread atual bloquear e envia uma notificação de erro para o depurador do IDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT HandleRuntimeError(  
   IActiveScriptErrorDebug*  pErrorDebug,  
   IActiveScriptSite*        pScriptSite,  
   BREAKRESUMEACTION*        pbra,  
   ERRORRESUMEACTION*        perra,  
   BOOL*                     pfCallOnScriptError  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pErrorDebug`  
 [in] O erro que ocorreu.  
  
 `pScriptSite`  
 [in] O site de script do thread.  
  
 `pbra`  
 [out] Ação a ser tomada quando o depurador retoma o aplicativo.  
  
 `perra`  
 [out] Ação a ser tomada quando o depurador retoma o aplicativo se houver um erro.  
  
 `pfCallOnScriptError`  
 [out] Sinalizador que é `TRUE` se o mecanismo deve chamar o `IActiveScriptSite::OnScriptError` método.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Um mecanismo de linguagem chama esse método no contexto de um thread que causa um erro de tempo de execução. Este método faz com que o thread atual bloquear e envia uma notificação de erro a ser enviada ao depurador do IDE. Quando o depurador IDE retoma o aplicativo, este método retorna com a ação a ser executada.  
  
> [!NOTE]
>  Enquanto estiver na falha de tempo de execução, o mecanismo de linguagem pode ser chamado pelo thread para executar tarefas, como enumerar os quadros de pilha ou avaliar expressões.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugApplication](../../winscript/reference/idebugapplication-interface.md)   
 [Interface IActiveScriptErrorDebug](../../winscript/reference/iactivescripterrordebug-interface.md)   
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)   
 [Enumeração BREAKRESUMEACTION](../../winscript/reference/breakresumeaction-enumeration.md)   
 [ERRORRESUMEACTION Enumeration](../../winscript/reference/errorresumeaction-enumeration.md)