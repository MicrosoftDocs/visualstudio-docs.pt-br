---
title: 'IScriptNode:: CreateChildEntry | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode. CreateChildEntry
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildEntry
ms.assetid: b9682505-4457-40e9-8691-235843637506
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8fcc010efe8fcf30a8f467dd94befff54bc5fac5
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729686"
---
# <a name="iscriptnode-createchildentry"></a>IScriptNode:: CreateChildEntry
Adiciona uma instância de filho de `IScriptEntry`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CreateChildEntry(  
   ULONG              isn,  
   DWORD              dwCookie,  
   LPCOLESTR          pszDelimiter,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `isn`  
 [in] O índice do filho no pai.  
  
 `dwCookie`  
 [in] Um valor definido pelo aplicativo usado para associar a entrada filho com o objeto de host.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final do bloco de script. Para análise, o host normalmente usa um delimitador (como duas aspas simples), para detectar o final do bloco de script.  
  
 O delimitador permite que o mecanismo para fornecer o pré-processamento de criação de script. Por exemplo, o mecanismo pode substituir uma aspa simples por duas aspas simples para uso como um delimitador. O mecanismo determina como o delimitador é usado.  
  
 Definido como NULL se um delimitador não marcar o fim do bloco de script.  
  
 `ppse`  
 [out] O endereço de uma variável que recebe um ponteiro para o `IScriptEntry` interface da instância filho.  
  
 Para `IScriptNode` objetos que representam uma página da Web, este parâmetro retorna um `IScriptEntry` instância que especifica um bloco de script.  
  
 Para `IScriptEntry` objetos que representam um bloco de script, este parâmetro retorna um `IScriptEntry` instância que especifica um objeto de função.  
  
 Para `IScriptEntry` objetos que representam uma função do objeto, esse método falhar.  
  
 Para `IScriptScriptlet` objetos, esse método falhar.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 O `IScriptNode` interface representa uma página da Web ou seus elementos. O `IScriptEntry` interface (que é derivada de `IScriptNode`) representa um bloco de script ou um objeto de função. O `IScriptScriptlet` interface (que é derivada de `IScriptEntry`) representa um manipulador de eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IScriptNode](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry Interface](../../winscript/reference/iscriptentry-interface.md)