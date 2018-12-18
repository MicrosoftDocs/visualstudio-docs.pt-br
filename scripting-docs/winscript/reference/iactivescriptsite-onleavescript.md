---
title: IActiveScriptSite::OnLeaveScript | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnLeaveScript
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnLeaveScript
ms.assetid: 79af0e22-fbe3-4fae-8a5f-7af8b857678d
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aba20c13dc5568165641c5c7b8e871e0b5e8f322
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725166"
---
# <a name="iactivescriptsiteonleavescript"></a>IActiveScriptSite::OnLeaveScript
Informa ao host que o mecanismo de script foi retornado de execução de código de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT OnLeaveScript(void);  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se houver êxito.  
  
## <a name="remarks"></a>Comentários  
 O mecanismo de script deve chamar esse método antes de devolver o controle para um aplicativo de chamada que inseriu o mecanismo de script. Por exemplo, se o script chama um objeto que dispara um evento tratado pelo mecanismo de script, o mecanismo de script deve chamar o [IActiveScriptSite::OnEnterScript](../../winscript/reference/iactivescriptsite-onenterscript.md) método antes de executar o evento e deve chamar `IActiveScriptSite::OnLeaveScript`depois de executar o evento antes de retornar para o objeto que disparou o evento. Chamadas para esse método podem ser aninhadas. Todas as chamadas para `IActiveScriptSite::OnEnterScript` requer uma chamada correspondente para esse método.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)