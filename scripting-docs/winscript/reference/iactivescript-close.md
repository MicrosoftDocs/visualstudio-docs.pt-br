---
title: IActiveScript::Close | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.Close
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_Close
ms.assetid: cc7dd63b-1d7e-410a-857b-09ea3aade275
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7c90b5d089ea6665060944e0a6f720a43aa1295a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24640966"
---
# <a name="iactivescriptclose"></a>IActiveScript::Close
Faz com que o mecanismo de script abandonar qualquer script carregado no momento, perder seu estado e liberar qualquer ponteiros de interface a outros objetos, portanto, entrar em um estado fechado. Coletores de eventos, o texto do script executado imediatamente e invocações de macro que já estão em andamento sejam concluídas antes das alterações de estado (use [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md) para cancelar um thread em execução do script). Esse método deve ser chamado pelo host criando antes que a interface seja liberada para evitar problemas de referência circular.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Close(void);  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|`S_OK`|Êxito.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script já estava no estado fechado).|  
|`OLESCRIPT_S_PENDING`|O método foi enfileirado com êxito, mas o estado ainda não foi alterado. Quando as alterações de estado, o site está para ser o retorno de chamada de [IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md) método.|  
|`S_FALSE`|O método foi bem-sucedido, mas o script já foi fechado.|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)