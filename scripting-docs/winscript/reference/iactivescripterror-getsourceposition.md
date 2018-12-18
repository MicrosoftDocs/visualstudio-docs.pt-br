---
title: IActiveScriptError::GetSourcePosition | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptError.GetSourcePosition
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptError_GetSourcePosition
ms.assetid: ae9b26b1-82a7-4645-9686-3261d8248664
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d63310a8ba5cfda39d48a482eaf7c345cd492adc
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645836"
---
# <a name="iactivescripterrorgetsourceposition"></a>IActiveScriptError::GetSourcePosition
Recupera o local no código-fonte em que ocorreu um erro enquanto o mecanismo de script estiver em execução em um script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetSourcePosition(  
    DWORD *pdwSourceContext,  // context cookie  
    ULONG *pulLineNumber,     // line number of error  
    LONG *pichCharPosition    // character position of error  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdwSourceContext`  
 [out] Endereço de uma variável que recebe um cookie que identifica o contexto. A interpretação deste parâmetro depende do aplicativo host.  
  
 `pulLineNumber`  
 [out] Endereço de uma variável que recebe o número da linha no arquivo de origem onde ocorreu o erro.  
  
 `pichCharPosition`  
 [out] Endereço de uma variável que recebe a posição do caractere na linha onde ocorreu o erro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se for bem-sucedido, ou `E_FAIL` se o local não foi recuperado.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptError](../../winscript/reference/iactivescripterror.md)