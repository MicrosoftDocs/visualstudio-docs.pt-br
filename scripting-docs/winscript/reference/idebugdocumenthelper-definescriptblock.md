---
title: IDebugDocumentHelper::DefineScriptBlock | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.DefineScriptBlock
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::DefineScriptBlock
ms.assetid: e4120377-f04f-44b1-950b-2beba06c9c12
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3b6ec86dacc2e3a8f3d9e28a6db744b778ff01eb
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726996"
---
# <a name="idebugdocumenthelperdefinescriptblock"></a>IDebugDocumentHelper::DefineScriptBlock
Indica o auxiliar que um determinado intervalo de caracteres é um bloco de script que é tratado pelo mecanismo de script específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT DefineScriptBlock(  
   ULONG           ulCharOffset,  
   ULONG           cChars,  
   IActiveScript*  pas,  
   BOOL            fScriptlet,  
   DWORD_PTR*      pdwSourceContext  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ulCharOffset`  
 [in] Local do início do bloco de script.  
  
 `cChars`  
 [in] Número de caracteres no bloco de script.  
  
 `pas`  
 [in] O mecanismo de script para este bloco de script.  
  
 `fScriptlet`  
 [in] Sinalizador que indica se o bloco de script é um miniscript.  
  
 `pdwSourceContext`  
 [out] O contexto de origem para o bloco de script.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Um host inteligente pode usar esse método quando seus documentos contêm blocos de script incorporado. Um mecanismo de linguagem pode usar esse método quando seu código contém scripts incorporados para outros idiomas.  
  
 O mecanismo de script é responsável por todas as sintaxe cores e o código de contexto pesquisas no bloco de script.  
  
 O `DefineScriptBlock` método deve ser chamado depois que o texto foi adicionado (por exemplo, usando o `IDebugDocumentHelper::AddDBCSText` método), mas antes do script foi analisado blocos (por exemplo, usando o `IActiveScriptParse ::ParseScriptText` método).  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugDocumentHelper](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper::AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)