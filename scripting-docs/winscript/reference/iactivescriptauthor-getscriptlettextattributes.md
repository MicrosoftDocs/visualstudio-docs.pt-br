---
title: IActiveScriptAuthor::GetScriptletTextAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetScriptletTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetScriptletTextAttributes
ms.assetid: 082edfce-6c5b-4e5e-b942-31b423a4fa1d
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b01fba7d0e8eb80fed51b1ff0ebd3a8816bacb01
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645686"
---
# <a name="iactivescriptauthorgetscriptlettextattributes"></a>IActiveScriptAuthor::GetScriptletTextAttributes
Retorna os atributos de texto de um miniscript.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetScriptletTextAttributes(  
   LPCOLESTR pszCode,  
   ULONG cch,  
   LPCOLESTR pszDelimiter,  
   DWORD dwFlags,  
   SOURCE_TEXT_ATTR *pattr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszCode`  
 [in, size_is (`cch`)] o texto miniscript. Essa cadeia de caracteres não precisa ser terminado em null.  
  
 `cch`  
 [in] O tamanho usado para o `pszCode` e `pattr` parâmetros.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final de miniscript. Quando `pszCode` é analisada em um fluxo de texto, o host normalmente usa um delimitador (como duas aspas simples), para detectar o fim do miniscript. Defina esse parâmetro como NULL se nenhum delimitador é usado para identificar o término do miniscript.  
  
 `dwFlags`  
 [in] Os sinalizadores que estão associados com os atributos de texto do miniscript. Pode ser uma combinação dos valores a seguir.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|Identificar os identificadores que têm o atributo SOURCETEXT_ATTR_IDENTIFIER e identificar os operadores de ponto que têm o atributo SOURCETEXT_ATTR_MEMBERLOOKUP.|  
|GETATTRFLAG_THIS|0x0100|Identificar o objeto atual que tem o atributo SOURCETEXT_ATTR_THIS.|  
|GETATTRFLAG_HUMANTEXT|0x8000|Identifique o texto de comentário e conteúdo de cadeia de caracteres que tem o atributo SOURCETEXT_ATTR_HUMANTEXT.|  
  
 `pattr`  
 [out no, size_is (`cch`)] as informações de cor para o código de miniscript.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptAuthor](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::GetScriptTextAttributes](../../winscript/reference/iactivescriptauthor-getscripttextattributes.md)   
 [SOURCE_TEXT_ATTR Enumeration](../../winscript/reference/source-text-attr-enumeration.md)