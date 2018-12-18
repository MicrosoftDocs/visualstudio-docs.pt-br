---
title: IActiveScriptAuthor::GetEventHandler | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetEventHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetEventHandler
ms.assetid: 87c7a71d-46b9-448c-b34d-394105e20982
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2b09f900162b6dba82696c946b53ab131691530c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645576"
---
# <a name="iactivescriptauthorgeteventhandler"></a>IActiveScriptAuthor::GetEventHandler
Retorna o miniscript que tem os atributos especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetEventHandler(  
   IDispatch          *pdisp,  
   LPCOLESTR          pszItem,  
   LPCOLESTR          pszSubItem,  
   LPCOLESTR          pszEvent,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdisp`  
 [in] O `IDispatch` que corresponde ao objeto de `NamedItem` à qual o miniscript está associado.  
  
 `pszItem`  
 [in] O endereço do buffer do identificador de nível superior do nome totalmente qualificado miniscript no host.  
  
 `pszSubItem`  
 [in] O endereço do buffer do identificador de segundo nível do nome totalmente qualificado miniscript no host. Definido como NULL se o nome tem apenas um nível.  
  
 `pszEvent`  
 [in] O endereço de um buffer que contém o nome do evento. O miniscript é um manipulador de eventos para esse evento.  
  
 `ppse`  
 [out] O endereço de uma variável que recebe um ponteiro para o `IScriptEntry` interface do miniscript que tem os atributos especificados.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptAuthor](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IScriptEntry Interface](../../winscript/reference/iscriptentry-interface.md)