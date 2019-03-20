---
title: IActiveScriptSite::OnStateChange | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnStateChange
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnStateChange
ms.assetid: 3e9c5cbe-ca8e-426a-84fd-04e9c2daac7e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad5719a93aec2940f1180a6ff45a028b937b0dfe
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58148640"
---
# <a name="iactivescriptsiteonstatechange"></a>IActiveScriptSite::OnStateChange
Informa ao host que o mecanismo de script foi alterado de estados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT OnStateChange(  
    SCRIPTSTATE ssScriptState  // new state of engine  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ssScriptState`  
 [in] Valor que indica o novo estado de script. Consulte a [IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md) método para obter uma descrição dos Estados.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se houver êxito.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)