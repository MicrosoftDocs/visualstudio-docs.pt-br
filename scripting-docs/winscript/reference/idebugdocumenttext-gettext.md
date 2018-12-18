---
title: IDebugDocumentText::GetText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetText
ms.assetid: 3c940a30-6c0f-4deb-aa4d-21a0bdef8461
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5a1006304974fab4959ad6313ffdc26793cdd345
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728076"
---
# <a name="idebugdocumenttextgettext"></a>IDebugDocumentText::GetText
Recupera os caracteres de e/ou os atributos de caracteres associados a um intervalo de posição do caractere.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetText(  
   ULONG              cCharacterPosition,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `cCharacterPosition`  
 [in] Local do intervalo de posição do caractere inicial.  
  
 `pcharText`  
 [out no] Um buffer de texto de caractere. O buffer deve ser grande o suficiente para manter `cMaxChars` caracteres. Se esse parâmetro for NULL, o método não retornar caracteres.  
  
 `pstaTextAttr`  
 [out no] Um buffer de atributo de caracteres. O buffer deve ser grande o suficiente para manter `cMaxChars` caracteres. Se esse parâmetro for NULL, o método não retorna atributos.  
  
 `pcNumChars`  
 [out no] O número de caracteres/atributos retornados. Esse parâmetro deve ser definido como zero antes de chamar esse método.  
  
 `cMaxChars`  
 [in] Número de caracteres no intervalo de posição de caractere. Também especifica o número máximo de caracteres a ser retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna os caracteres de e/ou os atributos de caracteres associados a um intervalo de posição do caractere. O intervalo de posição de caractere é especificado por uma posição de caractere e um número de caracteres.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugDocumentText](../../winscript/reference/idebugdocumenttext-interface.md)   
 [SOURCE_TEXT_ATTR Enumeration](../../winscript/reference/source-text-attr-enumeration.md)