---
title: IActiveScript::SetScriptState | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.SetScriptState
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_SetScriptState
ms.assetid: f2b2700c-0c8d-40db-ad84-dc751c5d9bc2
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 146cd5e4f2b6137fc6fe6e32e8ca153c3aab8fd5
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645666"
---
# <a name="iactivescriptsetscriptstate"></a>IActiveScript::SetScriptState
Coloca o mecanismo de script no estado indicado. Esse método pode ser chamado de threads não base sem resultando em um texto explicativo de base não a objetos de host ou para o [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) interface.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetScriptState(  
    SCRIPTSTATE ss  // identifier of new state  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ss`  
 [in] Define o mecanismo de script para o estado especificado. Pode ser um dos valores definidos no [enumeração SCRIPTSTATE](../../winscript/reference/scriptstate-enumeration.md) enumeração.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_FAIL`|O mecanismo de script não dá suporte a transição para o estado inicializado. O host deve descartar este mecanismo de script e criar, inicializar e carregar um novo mecanismo de script para obter o mesmo efeito.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado) e, portanto, a falha.|  
|`OLESCRIPT_S_PENDING`|O método foi enfileirado com êxito, mas o estado ainda não foi alterado. Quando as alterações de estado, o site será chamado novamente por meio de [IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md) método.|  
|`S_FALSE`|O método foi bem-sucedido, mas o script já estava no estado indicado.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre estados de mecanismo de script, consulte a seção de estados do mecanismo de Script de [mecanismos de Script do Windows](../../winscript/windows-script-engines.md) .  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript::Clone](../../winscript/reference/iactivescript-clone.md)   
 [IActiveScript::GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)   
 [IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md)   
 [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)