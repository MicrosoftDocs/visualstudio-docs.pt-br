---
title: IActiveScript::SetScriptSite | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.SetScriptSite
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_SetScriptSite
ms.assetid: 47d94c32-09f8-4539-ac56-0236026f627b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 11fa9003abb03c42adcbf3a548bb5b90d763a344
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645566"
---
# <a name="iactivescriptsetscriptsite"></a>IActiveScript::SetScriptSite
Informa ao mecanismo de script da [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) site interface fornecida pelo host. Chamar esse método antes de qualquer outro [IActiveScript](../../winscript/reference/iactivescript.md) métodos de interface é usada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetScriptSite(  
    IActiveScriptSite *pScriptSite  // address of host script site  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pScriptSite`  
 [in] Endereço do site do script fornecido pelo host a ser associado esta instância do mecanismo de script. O site deve ser atribuído exclusivamente para esta instância de mecanismo de script; ela não pode ser compartilhada com outros mecanismos de script.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_FAIL`|Ocorreu um erro não especificado; o mecanismo de script não pôde concluir a inicialização do site.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, um site já foi definido).|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)