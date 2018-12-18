---
title: IActiveScript::GetScriptThreadID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptThreadID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptThreadID
ms.assetid: 2595d76e-30b5-429f-88b4-1d026645dd9b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8850319035b7b5e3a9cbbd4bbe4340e1eefacc96
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641606"
---
# <a name="iactivescriptgetscriptthreadid"></a>IActiveScript::GetScriptThreadID
Recupera um script mecanismo-identificador definido para o thread associado o determinado thread Win32.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetScriptThreadID(  
    DWORD dwWin32ThreadID,       // Win32 thread identifier.  
    SCRIPTTHREADID *pstidThread  // Receives scripting thread. identifier  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwWin32ThreadID` ,  
 [in] Identificador de thread de thread Win32 em execução no processo atual. Use o [IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md) função para recuperar o identificador de thread do thread em execução no momento.  
  
 `pstidThread` ,  
 [out] Endereço de uma variável que recebe o identificador de thread de script associado o determinado thread Win32. A interpretação esse identificador é da esquerda para o mecanismo de script, mas pode ser apenas uma cópia do identificador de thread do Windows. Observe que, se o thread de Win32 terminar, este identificador se torna não atribuído e posteriormente pode ser atribuído a outro thread.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado) e, portanto, a falha.|  
  
## <a name="remarks"></a>Comentários  
 O identificador recuperado pode ser usado em chamadas subsequentes para métodos de controle de execução de thread de script, como o [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md) método.  
  
 Esse método pode ser chamado de threads não base sem resultando em um texto explicativo de base não a objetos de host ou para o [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)