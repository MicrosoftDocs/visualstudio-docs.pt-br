---
title: 'Método: Freevirtualmemory | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.FreeVirtualMemory
apilocation:
- jscript9diag.dll
ms.assetid: ea54bad3-9ae3-436b-974d-70fc7fffefd6
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3b53d7f80227a1c4eb0ef0293093543c09c5a367
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728736"
---
# <a name="ijsdebugdatatargetfreevirtualmemory-method"></a>Método IJsDebugDataTarget::FreeVirtualMemory
Libera e/ou decommits uma região de memória dentro do espaço de endereço virtual do processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT FreeVirtualMemory(  
   UINT64 address,  
   DWORD size,  
   DWORD freeType  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `address`  
 [in] Endereço dentro do processo de destino em que a memória deve ser liberada.  
  
 `size`  
 [in] Número de bytes a liberação. Para liberar uma região de memória, esse valor deve ser zero.  
  
 `freeType`  
 [in] Indica o tipo de operação livre a ser executada. Normalmente, isso é MEM_RELEASE (0x8000), que libera a região especificada de páginas. Após a operação, as páginas estão no estado livre. MEM_DECOMMIT (0x4000) pode ser usado em vez disso, a liberação de páginas sem liberá-los.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Para obter informações adicionais, consulte a API do Win32 VirtualFree.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)