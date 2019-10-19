---
title: 'IActiveScriptSiteDebug32:: GetDocumentContextFromPosition | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53348dff-35a6-4303-b263-90c10af06bf3
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 7acbe2a5741fa94ac42470a85803d1720e0a8fa1
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574842"
---
# <a name="iactivescriptsitedebug32getdocumentcontextfromposition"></a>IActiveScriptSiteDebug32::GetDocumentContextFromPosition
Usado pelo mecanismo de linguagem para delegar `IDebugCodeContext::GetSourceContext`.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetDocumentContextFromPosition(  
   DWORD_PTR                dwSourceContext,  
   ULONG                    uCharacterOffset,  
   ULONG                    uNumChars,  
   IDebugDocumentContext**  ppsc  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwSourceContext`  
 no O conteúdo de origem fornecido para `ParseScriptText` ou `AddScriptlet`.  
  
 `uCharacterOffset`  
 no Deslocamento de caractere relativo ao início do bloco de script ou do scriptlet.  
  
 `uNumChars`  
 no Número de caracteres neste contexto.  
  
 `ppsc`  
 fora O contexto do documento correspondente a este intervalo de posição de caractere.  
  
## <a name="return-value"></a>Valor retornado  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Os mecanismos de linguagem usam esse método para delegar `IDebugCodeContext::GetSourceContext`.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSiteDebug32 Interface](../../winscript/reference/iactivescriptsitedebug32-interface.md)