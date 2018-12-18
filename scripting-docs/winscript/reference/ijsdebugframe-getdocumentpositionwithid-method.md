---
title: 'Método: Getdocumentpositionwithid | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.GetDocumentPositionWithId
apilocation:
- jscript9diag.dll
ms.assetid: 48f8eb26-8ae4-4d5c-bd94-796023b03bcb
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f11e9ad51094522adec99ef82681f42ac500a251
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727726"
---
# <a name="ijsdebugframegetdocumentpositionwithid-method"></a>Método IJsDebugFrame::GetDocumentPositionWithId
Retorna a posição atual deste quadro de pilha dentro do documento de nível de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetDocumentPositionWithId(  
   UINT64 *pDocumentId,  
   DWORD *pCharacterOffset,  
   DWORD *pStatementCharCount  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pDocumentId`  
 [out] ID exclusiva para um documento de origem (ponteiro para o IDebugDocumentText).  
  
 `pCharacterOffset`  
 [out] O deslocamento de caractere com base em zero do início do script.  
  
 `pStatementCharCount`  
 [out] O comprimento da instrução atual, que inicia em * pCharacterOffset, em caracteres.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)