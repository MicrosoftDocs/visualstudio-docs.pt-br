---
title: IActiveScriptSite::OnScriptTerminate | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnScriptTerminate
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnScriptTerminate
ms.assetid: 3301ddf4-5929-404c-81d3-1a720e589008
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eef8bd2a3f2e2a4eb4fd4b5f0e35fcd9acfe5bc9
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724796"
---
# <a name="iactivescriptsiteonscriptterminate"></a>IActiveScriptSite::OnScriptTerminate
Informa ao host que o script tiver concluído a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT OnScriptTerminate(  
    VARIANT *pvarResult,   // address of script results  
    EXCEPINFO *pexcepinfo  // address of structure with exception information  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pvarResult`  
 [in] Endereço de uma variável que contém o resultado do script, ou `NULL` se o script não gerado nenhum resultado.  
  
 `pexcepinfo`  
 [in] Endereço de um `EXCEPINFO` estrutura que contém informações de exceção geradas quando o script foi finalizado, ou `NULL` se nenhuma exceção foi gerada.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se houver êxito.  
  
## <a name="remarks"></a>Comentários  
 O mecanismo de script chama esse método antes da chamada para o [IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md) método, com a definição do sinalizador SCRIPTSTATE_INITIALIZED seja concluído. Esse método pode ser usado para retornar o status de conclusão e os resultados para o host. Observe que muitas linguagens de script, que se baseiam em recebendo eventos do host, têm intervalos de vida que são definidos pelo host. Nesse caso, esse método não pode ser chamado.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)