---
title: IActiveScriptDebug::GetScriptTextAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptDebug.GetScriptTextAttributes
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptDebug::GetScriptTextAttributes
ms.assetid: 2e8bda34-db0c-4b2e-a17f-82c4e0dbbc8c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c8e9cd76da3e754eabce836b386893043dcd0622
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645846"
---
# <a name="iactivescriptdebuggetscripttextattributes"></a>IActiveScriptDebug::GetScriptTextAttributes
Retorna os atributos de texto de um bloco arbitrário de texto de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetScriptTextAttributes(  
   LPCOLESTR          pstrCode,  
   ULONG              uNumCodeChars,  
   LPCOLESTR          pstrDelimiter,  
   DWORD              dwFlags,  
   SOURCE_TEXT_ATTR*  pattr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrCode`  
 [in] O texto de bloco de script. Essa cadeia de caracteres não precisa ser terminado em null.  
  
 `uNumCodeChars`  
 [in] O número de caracteres no texto do bloco de script.  
  
 `pstrDelimiter`  
 [in] Endereço do delimitador final do bloco de script. Quando `pstrCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do bloco de script. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional pré-processamento primitivo (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o mecanismo de script usa essas informações dependem do mecanismo de script. Defina esse parâmetro como NULL se o host não tiver usado um delimitador para marcar o fim do bloco de script.  
  
 `dwFlags`  
 [in] Sinalizadores associados com o bloco de script. Pode ser uma combinação desses valores:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|GETATTRTYPE_DEPSCAN|0x0001|Indica que os identificadores e ponto deve ser identificados com os sinalizadores SOURCETEXT_ATTR_IDENTIFIER e SOURCETEXT_ATTR_MEMBERLOOKUP, respectivamente.|  
|GETATTRFLAG_THIS|0x0100|Indica que o identificador para o objeto atual deve ser identificado com o sinalizador SOURCETEXT_ATTR_THIS.|  
|GETATTRFLAG_HUMANTEXT|0x8000|Indica que o texto de comentário e conteúdo de cadeia de caracteres deve ser identificado com o sinalizador SOURCETEXT_ATTR_HUMANTEXT.|  
  
 `pattr`  
 [out no] Buffer para conter os atributos retornados.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Um host inteligente que implementa `IDebugDocumentText` interface pode usar esse método para delegar a chamadas para o `IDebugDocumentText::GetText` método.  
  
 Esse método para blocos de script; o `GetScriptletTextAttributes` método é para miniscripts.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptDebug](../../winscript/reference/iactivescriptdebug-interface.md)   
 [IActiveScriptDebug::GetScriptletTextAttributes](../../winscript/reference/iactivescriptdebug-getscriptlettextattributes.md)   
 [Interface IDebugDocumentText](../../winscript/reference/idebugdocumenttext-interface.md)   
 [IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)   
 [SOURCE_TEXT_ATTR Enumeration](../../winscript/reference/source-text-attr-enumeration.md)