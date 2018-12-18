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
- IJsDebugDataTarget.WriteMemory
apilocation:
- jscript9diag.dll
ms.assetid: 0d3c04c3-9ef8-4842-a145-3d29bca75062
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ed562c1cbdd645da6cca87e45f272c25f8bc0d4b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727896"
---
# <a name="ijsdebugdatatargetwritememory-method"></a>Método IJsDebugDataTarget::WriteMemory
Lê a memória do processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT WriteMemory(  
   UINT64 address,  
   const BYTE *pMemory,  
   DWORD size  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `address`  
 [in] O endereço base do qual gravar a memória do processo de destino.  
  
 `pMemory`  
 [in] Os dados a serem gravados no espaço de endereço de processo especificado.  
  
 `size`  
 [in] O número de bytes a serem gravados para o processo.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Antes que ocorra a transferência de dados, o sistema verifica se todos os dados no endereço básico e a memória do tamanho especificado está acessível para acesso de gravação e se não estiver acessível, a função gerará um erro de E_JsDEBUG_INVALID_MEMORY_ADDRESS.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)