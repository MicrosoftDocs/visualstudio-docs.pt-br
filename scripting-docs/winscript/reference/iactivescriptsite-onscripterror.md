---
title: 'IActiveScriptSite:: OnScriptError | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnScriptError
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnScriptError
ms.assetid: 5c9c85cc-21ad-4232-be83-a24cc7570108
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9f0078b53515a881d7f2ac1475cf5565fa22a025
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570277"
---
# <a name="iactivescriptsiteonscripterror"></a>IActiveScriptSite::OnScriptError
Informa ao host que ocorreu um erro de execução enquanto o mecanismo estava executando o script.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT OnScriptError(  
    IActiveScriptError *pase  // address of error interface  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pase`  
 no Endereço da interface [IActiveScriptError](../../winscript/reference/iactivescripterror.md) do objeto de erro. Um host pode usar essa interface para obter informações sobre o erro de execução.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna `S_OK` se o erro foi manipulado corretamente ou um código de erro definido por OLE, caso contrário.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)