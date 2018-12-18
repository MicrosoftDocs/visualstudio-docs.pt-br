---
title: IActiveScriptAuthor::GetLanguageFlags | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetLanguageFlags
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetLanguageFlags
ms.assetid: eb244452-62f7-4a73-b48f-1aa05cbcc32d
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6137f1cd77d2f305a9ff9d51ac49c214e4c4237b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645536"
---
# <a name="iactivescriptauthorgetlanguageflags"></a>IActiveScriptAuthor::GetLanguageFlags
Retorna informações de idioma.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetLanguageFlags(  
   DWORD              *pgrfasa  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pgrfasa`  
 [out] Os sinalizadores que contêm informações de idioma. Pode ser uma combinação dos seguintes valores:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|fasaPreferInternalHandler|0x0001|O idioma prefere a criação de manipulador de eventos de script pelo script de criação de mecanismo, em vez do aplicativo.|  
|fasaSupportInternalHandler|0x0002|A linguagem dá suporte a manipuladores de eventos de script criados pelo script do mecanismo de criação.|  
|fasaCaseSensitive|0x0004|A linguagem de script diferencia maiusculas de minúsculas.|  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Se o mecanismo de criação de script gerencia manipuladores de eventos, seu aplicativo deve chamar `CreateChildHandler` de um `IScriptEntry` objeto. Isso cria uma `IScriptScriptlet` objeto corresponde ao manipulador de eventos. O mecanismo também adiciona um manipulador de eventos para a entrada de script. O manipulador de eventos é uma função vazia que contém as informações de assinatura especificada.  
  
 Se seu aplicativo gerencia manipuladores de eventos, é necessário chamar `CreateChildHandler` de um `IScriptNode` objeto que representa um miniscript de manipulador de eventos. Isso cria uma `IScriptScriptlet` objeto que está associado com o miniscript do manipulador de eventos. O aplicativo também precisa adicionar uma função vazia como um evento de manipulador para uma nova ou existente `IScriptEntry` objeto.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptAuthor Interface](../../winscript/reference/iactivescriptauthor-interface.md)