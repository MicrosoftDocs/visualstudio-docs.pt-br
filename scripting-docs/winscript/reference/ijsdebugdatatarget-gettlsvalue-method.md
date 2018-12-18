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
- IJsDebugDataTarget.GetTlsValue
apilocation:
- jscript9diag.dll
ms.assetid: db575be9-7b24-45c5-9008-e4f2f76d6757
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4205adfb24a1a64d4e90f3fdcaf5a5ecbc4028de
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727876"
---
# <a name="ijsdebugdatatargetgettlsvalue-method"></a>Método IJsDebugDataTarget::GetTlsValue
Para o thread que está sendo depurado, recupera o valor no slot thread (TLS) de armazenamento local para o índice especificado do TLS.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetTlsValue(  
   DWORD threadId,  
   UINT32 tlsIndex,  
   UINT64 *pValue  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `threadId`  
 [in] Em execução no processo de destino para ler a partir do thread.  
  
 `tlsIndex`  
 [in] O índice TLS que foi alocado quando a função TlsAlloc chamado, o processo de destino.  
  
 `pValue`  
 [out] O valor de tamanho de ponteiro que foi armazenado no slot TLS do thread. Se o thread de destino é de 32 bits, 32-bits superiores desse valor será zero.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Cada thread de um processo tem seu próprio slot para cada índice TLS.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)