---
title: IEnumRemoteDebugApplicationThreads::Next | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumRemoteDebugApplicationThreads.Next
apilocation:
- pdm.dll
helpviewer_keywords:
- IEnumRemoteDebugApplicationThreads::Next
ms.assetid: d8d10d7e-3468-49be-acf9-d842db9940e7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d8ce0dc7c77cd3b58f388ab63a9d5a3573c93419
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729126"
---
# <a name="ienumremotedebugapplicationthreadsnext"></a>IEnumRemoteDebugApplicationThreads::Next
O `Next` método recupera um número de segmentos na sequência de enumeração especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Next(  
   ULONG                            celt,  
   IRemoteDebugApplicationThread**  pprdat,  
   ULONG*                           pceltFetched  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `celt`  
 [in] O número de segmentos para recuperar.  
  
 `pprdat`  
 [out] Retorna uma matriz de `IRemoteDebugApplicationThread` interfaces que representa os segmentos que estão sendo recuperados.  
  
 `pceltFetched`  
 [out] O número real de segmentos buscadas pelo enumerador.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna um número especificado de segmentos na sequência de enumeração.  
  
## <a name="see-also"></a>Consulte também  
 [IEnumRemoteDebugApplicationThreads Interface](../../winscript/reference/ienumremotedebugapplicationthreads-interface.md)