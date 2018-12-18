---
title: IActiveScriptAuthorProcedure::ParseProcedureText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthorProcedure.ParseProcedureText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthorProcedure::ParseProcedureText
ms.assetid: cb6c29c5-c749-48d7-a6a8-ccbf0f9119ec
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b9c4a1ba03a8498dbaa857dc5dbabba8914e54a8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645636"
---
# <a name="iactivescriptauthorprocedureparseproceduretext"></a>IActiveScriptAuthorProcedure::ParseProcedureText
Analisa um procedimento de código, adiciona o texto do procedimento de código para o mecanismo de criação de script e cria um `IScriptEntry` objeto correspondente para o procedimento de código.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ParseProcedureText(  
   LPCOLESTR   pszCode,  
   LPCOLESTR   pszFormalParams,  
   LPCOLESTR   pszProcedureName,  
   LPCOLESTR   pszItemName,  
   LPCOLESTR   pszDelimiter,  
   DWORD       dwCookie,  
   DWORD       dwFlags,  
   IDispatch   *pdispFor  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszCode`  
 [in] O texto do script para analisar.  
  
 `pszFormalParams`  
 [in] O endereço dos nomes de parâmetro formal para o procedimento. Os nomes de parâmetro devem ser separados pelos delimitadores apropriados para o mecanismo de criação de script. Os nomes não devem ser incluídos entre parênteses.  
  
 `pszProcedureName`  
 [in] O endereço do nome do procedimento a ser analisada.  
  
 `pszItemName`  
 [in] O endereço do buffer que contém o nome do item associado a `IScriptEntry` objeto.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final do bloco de script. Quando `pszCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador (como duas aspas simples), para detectar o final do bloco de script. Defina esse parâmetro como NULL se não houver nenhum delimitador para marcar o fim do bloco de script.  
  
 `dwCookie`  
 [in] Um valor definido pelo aplicativo que está associado com o novo `IScriptEntry` objeto.  
  
 `dwFlags`  
 [in] Não usado.  
  
 `pdispFor`  
 [in] Não usado.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Atual [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] mecanismo não implementa esse método.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptAuthorProcedure Interface](../../winscript/reference/iactivescriptauthorprocedure-interface.md)