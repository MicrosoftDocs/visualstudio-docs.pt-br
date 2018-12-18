---
title: IActiveScriptAuthor::GetScriptTextAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetScriptTextAttributes
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetScriptTextAttributes
ms.assetid: a53451de-cc5c-4b53-8e5f-81e196364caf
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6aa96623b4356f0a3d17c8b2631840953dac2d51
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645516"
---
# <a name="iactivescriptauthorgetscripttextattributes"></a>IActiveScriptAuthor::GetScriptTextAttributes
Retorna os atributos de texto para um bloco de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetScriptTextAttributes(  
    LPCOLESTR        pszCode,  
    ULONG            cch,  
    LPCOLESTR        pszDelimiter,  
    DWORD            dwFlags,  
    SOURCE_TEXT_ATTR *pattr);  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszCode`  
 [in, size_is (`cch`)] o texto do bloco de script. Essa cadeia de caracteres não precisa ser terminado em null.  
  
 `cch`  
 [in] O tamanho usado para o `pszCode` e `pattr` parâmetros.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final do script. Quando `pszCode` é analisada em um fluxo de texto, o host normalmente usa um delimitador (como duas aspas simples), para detectar o fim do miniscript. Defina esse parâmetro como NULL se não houver nenhum delimitador para identificar o fim do bloco de script.  
  
 `dwFlags`  
 [in] Os sinalizadores que estão associados com os atributos de texto do bloco de script. Pode ser uma combinação dos seguintes valores:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|Identificar os identificadores que têm o atributo SOURCETEXT_ATTR_IDENTIFIER e identificar os operadores de ponto que têm o atributo SOURCETEXT_ATTR_MEMBERLOOKUP.|  
|GETATTRFLAG_THIS|0x0100|Identificar o objeto atual que tem o atributo SOURCETEXT_ATTR_THIS.|  
|GETATTRFLAG_HUMANTEXT|0x8000|Identifique o texto de comentário e conteúdo de cadeia de caracteres que tem o atributo SOURCETEXT_ATTR_HUMANTEXT.|  
  
 `pattr`  
 [out no, size_is (`cch`)] as informações de cor para o código do bloco de script.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptAuthor](../../winscript/reference/iactivescriptauthor-interface.md)   
 [SOURCE_TEXT_ATTR Enumeration](../../winscript/reference/source-text-attr-enumeration.md)