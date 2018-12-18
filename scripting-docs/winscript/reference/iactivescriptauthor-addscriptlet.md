---
title: IActiveScriptAuthor::AddScriptlet | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddScriptlet
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddScriptlet
ms.assetid: 879a6651-f187-4934-b130-c1247549900b
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b21f906a73a313bf775683ba63738adb25af0007
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645656"
---
# <a name="iactivescriptauthoraddscriptlet"></a>IActiveScriptAuthor::AddScriptlet
Adiciona um miniscript de código como um filho do nível raiz `IScriptNode` objeto. No host, o nome totalmente qualificado do miniscript é permitido ter apenas dois níveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT AddScriptlet(  
   LPCOLESTR pszDefaultName,  
   LPCOLESTR pszCode,  
   LPCOLESTR pszItemName,  
   LPCOLESTR pszSubItemName,  
   LPCOLESTR pszEventName,  
   LPCOLESTR pszDelimiter,  
   DWORD dwCookie,  
   DWORD dwFlags  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszDefaultName`  
 [in] O endereço do nome padrão para associar o miniscript.  
  
 `pszCode`  
 [in] O endereço do texto miniscript.  
  
 `pszItemName`  
 [in] O endereço do buffer do identificador de nível superior do nome totalmente qualificado miniscript no host.  
  
 `pszSubItemName`  
 [in] O endereço do buffer do identificador de segundo nível do nome totalmente qualificado miniscript no host. Definido como NULL se o nome tem apenas um nível.  
  
 `pszEventName`  
 [in] O endereço de um buffer que contém o nome do evento para o qual o miniscript é um manipulador de eventos.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final do bloco de script. Quando `pszCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador (como duas aspas simples), para detectar o final do bloco de script. Defina esse parâmetro como NULL se um delimitador não marcar o fim do bloco de script.  
  
 `dwCookie`  
 [in] Um valor definido pelo aplicativo que é usado para associar o miniscript um objeto de host.  
  
 `dwFlags`  
 [in] Não usado.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptAuthor Interface](../../winscript/reference/iactivescriptauthor-interface.md)