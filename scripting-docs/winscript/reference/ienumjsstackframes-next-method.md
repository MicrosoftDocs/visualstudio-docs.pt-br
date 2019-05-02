---
title: 'Método ienumjsstackframes:: Next | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumJsStackFrames.Next
apilocation:
- jscript9diag.dll
ms.assetid: efceb3a1-9239-4f55-9cbb-94670679988b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94e3f478654fadec152aba0690a5474ebbfe02f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963293"
---
# <a name="ienumjsstackframesnext-method"></a>Método IEnumJsStackFrames::Next
Obtém o número especificado de quadros.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT Next(  
   ULONG cFrameCount,  
   JS_NATIVE_FRAME *pFrames,  
   ULONG *pcFetched  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `cFrameCount`  
 [in] O número de quadros a serem obtidos.  
  
 `pFrames`  
 [out] A matriz para armazenar os quadros.  
  
 `pcFetched`  
 [out] O número de quadros retornados.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IEnumJsStackFrames](../../winscript/reference/ienumjsstackframes-interface.md)