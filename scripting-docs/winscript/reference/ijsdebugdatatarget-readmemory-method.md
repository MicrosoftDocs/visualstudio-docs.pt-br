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
- IJsDebugDataTarget.ReadMemory
apilocation:
- jscript9diag.dll
ms.assetid: 664e0f7d-2007-45f4-b993-36fe8b1944e5
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fc1b67b33e17761a675d6ced9e175b4206ede2e1
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728496"
---
# <a name="ijsdebugdatatargetreadmemory-method"></a>Método IJsDebugDataTarget::ReadMemory
Lê a memória do processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ReadMemory(  
   UINT64 address,  
   JsDebugReadMemoryFlags flags,  
   BYTE *pBuffer,  
   DWORD size,  
   DWORD *pBytesRead  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `address`  
 [in] O endereço base do qual ler a memória do processo de destino.  
  
 `flags`  
 [in] Sinalizadores de controlar o comportamento de ReadMemory.  
  
 `pBuffer`  
 [out] Um buffer que recebe o conteúdo do espaço de endereço do processo de destino. Em caso de falha, o conteúdo desse buffer não for especificado.  
  
 `size`  
 [in] O número de bytes a ser lido do processo.  
  
 `pBytesRead`  
 [out] Indica o número de bytes lidos do processo de destino. Se JsDebugAllowPartialRead estiver desmarcada, em caso de sucesso esse valor sempre será exatamente igual ao tamanho de entrada. Se JsDebugAllowPartialRead for especificado, em caso de sucesso, este valor será maior que zero.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Retorna S_OK bem-sucedido e códigos de falha é usada para qualquer erro. Retorna E_JsDEBUG_INVALID_MEMORY_ADDRESS se o endereço não é válido. Para obter mais informações, consulte JsDebugAllowPartialRead.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)