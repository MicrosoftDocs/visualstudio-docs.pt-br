---
title: 'Método Ijsdebugdatatarget: | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.GetThreadContext
apilocation:
- jscript9diag.dll
ms.assetid: faf2a689-6c49-4a7d-b5a6-2b323e2257a7
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4e2f858c66eda2ad09b04d7beab776c793b6f195
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728176"
---
# <a name="ijsdebugdatatargetgetthreadcontext-method"></a>Método IJsDebugDataTarget::GetThreadContext
Recupera o contexto de dado thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetThreadContext(  
   DWORD threadId,  
   ULONG32 contextFlags,  
   ULONG32 contextSize,  
   void *pContext  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `threadId`  
 [in] Thread em execução no processo de destino.  
  
 `contextFlags`  
 [in] Especifica os sinalizadores de contexto. Isso é o mesmo que o campo ContextFlags de contexto (para obter mais informações, Winnt. h de consulte, pesquise CONTEXT_ALL).  
  
 `contextSize`  
 [in] O tamanho do buffer especificado por pContext.  
  
 `pContext`  
 [out] Recebe a estrutura de contexto específico de plataforma para o buffer especificado por pContext.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)