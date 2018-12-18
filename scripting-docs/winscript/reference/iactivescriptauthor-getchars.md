---
title: IActiveScriptAuthor::GetChars | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetChars
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetChars
ms.assetid: a73ba263-12f7-4d5f-b4c8-9ad7e2d5d3cb
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: abc9c819c2dd4a75d6223af86b4fe89baebc186b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645646"
---
# <a name="iactivescriptauthorgetchars"></a>IActiveScriptAuthor::GetChars
Retorna o conjunto de caracteres de preenchimento para um contexto de conclusão solicitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetChars(  
   DWORD            fRequestedList,  
   BSTR             *pbstrChars  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `fRequestedList`  
 [in] O contexto de conclusão solicitada.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|0x0001|Solicitações de enumeração do lado esquerdo.|  
|SCRIPT_CMPL_MEMBER_TRIGGER|0x0002|Solicita o contexto de conclusão de membro.|  
|SCRIPT_CMPL_PARAM_TRIGGER|0x0003|Solicita a lista de parâmetros.|  
|SCRIPT_CMPL_COMMIT|0x0004|Conclusão de solicitações da lista de parâmetros.|  
  
 `pbstrChars`  
 [out] Os caracteres que correspondem ao contexto de conclusão solicitada.  
  
|Parâmetro `fRequestedList`|Caracteres retornados|  
|--------------------------------|-------------------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|"."|  
|SCRIPT_CMPL_MEMBER_TRIGGER|"="|  
|SCRIPT_CMPL_PARAM_TRIGGER|"(,"|  
|SCRIPT_CMPL_COMMIT|"()"|  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptAuthor Interface](../../winscript/reference/iactivescriptauthor-interface.md)