---
title: 'Método: Allocatevirtualmemory | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.AllocateVirtualMemory
apilocation:
- jscript9diag.dll
ms.assetid: 1d3a77b0-c1de-4a0c-a759-3e0c68fd96dd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 65b29bbf9a3405bcfab779bd877f798a863538d5
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728396"
---
# <a name="ijsdebugdatatargetallocatevirtualmemory-method"></a>Método IJsDebugDataTarget::AllocateVirtualMemory
Reserva e/ou confirma uma região de memória dentro do espaço de endereço virtual do processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT AllocateVirtualMemory(  
   UINT64 address,  
   DWORD size,  
   DWORD allocationType,  
   DWORD pageProtection,  
   UINT64 *pAllocatedAddress  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `address`  
 [in] O endereço dentro do processo de destino em que a memória deve ser confirmada ou reservada. Normalmente, esse valor é zero, caso o sistema escolhe um endereço.  
  
 `size`  
 [in] O tamanho da região de memória a ser alocada em bytes. O sistema será automaticamente arredondar para o próximo limite de página.  
  
 `allocationType`  
 [in] Indica o tipo de alocação para executar. Isso é normalmente MEM_COMMIT &#124; MEM_RESERVE (0x3000) que reserva e confirma uma alocação em uma única etapa.  
  
 `pageProtection`  
 [in] A proteção de memória para a região de páginas a serem alocados. Se as páginas estiverem sendo confirmadas, você pode especificar qualquer uma das constantes de proteção de memória (por exemplo, PAGE_READWRITE, PAGE_EXECUTE).  
  
 `pAllocatedAddress`  
 [out] Endereço base da região de páginas alocada.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 A função inicializa a memória aloca a zero, a menos que MEM_RESET é usado. Para obter informações adicionais, consulte a API do Win32 VirtualAlloc.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)