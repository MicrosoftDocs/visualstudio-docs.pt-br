---
title: IDebugDocumentHost::GetDeferredText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetDeferredText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetDeferredText
ms.assetid: 527da666-fef5-4db3-a319-e68d466a7721
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ace3bdbfef143a3307d81455788a1e81788cb50b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727116"
---
# <a name="idebugdocumenthostgetdeferredtext"></a>IDebugDocumentHost::GetDeferredText
Retorna um intervalo de caracteres que foram adicionados usando o `IDebugDocumentHelper::AddDeferredText` método no documento original do host.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetDeferredText(  
   DWORD              dwTextStartCookie,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwTextStartCookie`  
 [in] Cookie definido pelo host que representa a posição inicial do texto.  
  
 `pcharText`  
 [out no] Um buffer de texto de caractere. Esse método não retornar caracteres se esse parâmetro for `NULL`.  
  
 `pstaTextAttr`  
 [out no] Um buffer de atributo de caracteres. Este método não retorna atributos se esse parâmetro for `NULL`.  
  
 `pcNumChars`  
 [out no] Indica o número real de caracteres/atributos retornado. Esse parâmetro deve ser definido como zero antes de chamar esse método.  
  
 `cMaxChars`  
 [in] O número máximo de caracteres a ser retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_NOTIMPL`|O método não está implementado.|  
  
## <a name="remarks"></a>Comentários  
 Esse método pode retornar `E_NOTIMPL`, se o host não pode ser chamado `IDebugDocumentHelper::AddDeferredText`.  
  
> [!NOTE]
>  Esse método retorna o texto do documento original. O host não manter o controle de edição ou outras alterações no documento.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugDocumentHost](../../winscript/reference/idebugdocumenthost-interface.md)   
 [IDebugDocumentHelper::AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)   
 [SOURCE_TEXT_ATTR Enumeration](../../winscript/reference/source-text-attr-enumeration.md)