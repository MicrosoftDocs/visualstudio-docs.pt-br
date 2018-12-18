---
title: 'Método: Getdocumentposition | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJSDebugBreakPoint.GetDocumentPosition
apilocation:
- jscript9diag.dll
ms.assetid: 886df8ba-a59a-48a7-87f2-3b669e71528f
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c33751b0173626814f042fdc54a7d496b644573
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727606"
---
# <a name="ijsdebugbreakpointgetdocumentposition-method"></a>Método IJsDebugBreakPoint::GetDocumentPosition
Retorna a posição da instrução em que o ponto de interrupção foi vinculado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetDocumentPosition(  
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
 [Interface IJsDebugBreakPoint](../../winscript/reference/ijsdebugbreakpoint-interface.md)