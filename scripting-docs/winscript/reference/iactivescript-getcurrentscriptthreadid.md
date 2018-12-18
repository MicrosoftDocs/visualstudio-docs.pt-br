---
title: IActiveScript::GetCurrentScriptThreadID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetCurrentScriptThreadID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetCurrentScriptThreadID
ms.assetid: b09e8b48-4209-480e-8b71-e99ee9ae2e17
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5921dc4d0f9a9bf0d505fece0f47354cb16d440c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24640786"
---
# <a name="iactivescriptgetcurrentscriptthreadid"></a>IActiveScript::GetCurrentScriptThreadID
Recupera um script mecanismo-identificador definido para o thread em execução no momento. O identificador pode ser usado em chamadas subsequentes para métodos de controle de execução de thread de script, como o [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetCurrentScriptThreadID(  
    SCRIPTTHREADID *pstidThread  // receives scripting thread identifier  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstidThread`  
 [out] Endereço de uma variável que recebe o identificador de thread de script associado ao segmento atual. A interpretação esse identificador é da esquerda para o mecanismo de script, mas pode ser apenas uma cópia do identificador de thread do Windows. Se o thread de Win32 termina, esse identificador se torna não atribuído e subsequentemente pode ser atribuído a outro thread.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se for bem-sucedido, ou `E_POINTER` se um ponteiro inválido foi especificado.  
  
## <a name="remarks"></a>Comentários  
 Esse método pode ser chamado de threads não base sem resultando em um texto explicativo de base não a objetos de host ou para o [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)