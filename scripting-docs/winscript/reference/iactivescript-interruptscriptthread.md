---
title: IActiveScript::InterruptScriptThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.InterruptScriptThread
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_InterruptScriptThread
ms.assetid: 2304d035-6d39-4811-acd3-8a9640fdbef6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad717ee950dda4f0f0d7a14292f0f5f150ab4973
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641846"
---
# <a name="iactivescriptinterruptscriptthread"></a>IActiveScript::InterruptScriptThread
Interrompe a execução de um thread em execução do script (um coletor de eventos, a execução imediata ou uma chamada de macro). Esse método pode ser usado para finalizar um script que está preso (por exemplo, em um loop infinito). Ele pode ser chamado de threads não base sem resultando em um texto explicativo de base não a objetos de host ou para o [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT InterruptScriptThread(  
    SCRIPTTHREADID   stidThread,  // identifier of thread  
    const EXCEPINFO *pexcepinfo,  // receives error information  
    DWORD dwFlags  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `stidThread`  
 [in] Identificador do segmento para interrupção ou um dos seguintes valores de identificador de thread especial:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTTHREADID_ALL|Todos os threads. A interrupção é aplicada a todos os métodos de script está em andamento. Observe que, a menos que o chamador solicitou que o script a ser desconectada, o próximo evento de script faz com que o código de script para executar novamente chamando o [IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md) método com o SCRIPTSTATE_DISCONNECTED ou O sinalizador SCRIPTSTATE_INITIALIZED definido.|  
|SCRIPTTHREADID_BASE|O thread de base; ou seja, o thread em que o script do mecanismo foi instanciado.|  
|SCRIPTTHREADID_CURRENT|O thread em execução no momento.|  
  
 `pexcepinfo`  
 [in] Endereço de um `EXCEPINFO` estrutura que contém as informações de erro devem ser relatadas para o script anulado.  
  
 `dwFlags`  
 [in] Sinalizadores de opção associados com a interrupção. Pode ser um destes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTINTERRUPT_DEBUG|Se suportado, insira o depurador do mecanismo de script no ponto atual de execução do script.|  
|SCRIPTINTERRUPT_RAISEEXCEPTION|Se o suporte para a linguagem do mecanismo de script, permitem que o script de lidar com a exceção. Caso contrário, o método de script será anulado e o código de erro é retornado ao chamador; ou seja, o evento fonte ou macro chamador.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)