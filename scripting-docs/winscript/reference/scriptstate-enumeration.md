---
title: Enumeração SCRIPTSTATE | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTSTATE
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTSTATE enum
ms.assetid: 5f5deb05-c4bb-4964-8077-e624c6b2a14e
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 35e062a9c2f3076144063ffb77895c8a03ecc4ac
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734276"
---
# <a name="scriptstate-enumeration"></a>Enumeração SCRIPTSTATE
Especifica o estado de um mecanismo de script. Essa enumeração é usada pelo [IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md) , [IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md) , e [IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md) métodos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum tagSCRIPTSTATE {  
    SCRIPTSTATE_UNINITIALIZED = 0,  
    SCRIPTSTATE_INITIALIZED   = 5,  
    SCRIPTSTATE_STARTED       = 1,  
    SCRIPTSTATE_CONNECTED     = 2,  
    SCRIPTSTATE_DISCONNECTED  = 3,  
    SCRIPTSTATE_CLOSED        = 4  
} SCRIPTSTATE;  
```  
  
## <a name="enumeration-values"></a>Valores de enumeração  
  
|||  
|-|-|  
|SCRIPTSTATE_UNINITIALIZED|Script foi criado, mas ainda não foi inicializada usando um `IPersist*` interface e [IActiveScript::SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md) .|  
|SCRIPTSTATE_INITIALIZED|Script foi inicializado, mas não está em execução (conectar-se a outros objetos ou recebendo eventos) ou executar qualquer código. Código pode ser consultado para execução chamando o [IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md) método.|  
|SCRIPTSTATE_STARTED|Script pode executar o código, mas ainda não está recebendo os eventos de objetos adicionados pelo [IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) método.|  
|SCRIPTSTATE_CONNECTED|Script é carregado e conectado para recebendo eventos.|  
|SCRIPTSTATE_DISCONNECTED|Script é carregado e tem um estado de tempo de execução, mas desconectado temporariamente recebendo eventos.|  
|SCRIPTSTATE_CLOSED|Script foi fechado. O mecanismo de script não funciona e retorna erros para a maioria dos métodos.|  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e códigos de erro do script ativo](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)