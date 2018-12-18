---
title: Enumeração JsDebugReadMemoryFlags | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- JsDebugReadMemoryFlags
apilocation:
- jscript9diag.dll
ms.assetid: 0d98d154-9cb1-49de-b2df-a2d029d343b7
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7efb5170bf0314e95b1acded39a897c2236a29ff
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733706"
---
# <a name="jsdebugreadmemoryflags-enumeration"></a>Enumeração JsDebugReadMemoryFlags
Sinaliza para especificar o comportamento ao ler a memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
enum JsDebugReadMemoryFlags{   None = 0,   JsDebugAllowPartialRead= 0x1} JsDebugReadMemoryFlags;  
```  
  
## <a name="members"></a>Membros  
  
### <a name="values"></a>Valores  
  
|Nome|Descrição|  
|----------|-----------------|  
|`JsDebugAllowPartialRead`|Indica que o chamador deseja que a operação de leitura seja bem-sucedida se apenas parte da memória lido com êxito. Se isso for definido, um erro de E_JsDEBUG_INVALID_MEMORY_ADDRESS só será gerado se o 'Endereço' é inválido. Se esse sinalizador estiver desmarcado, será gerado um erro E_JsDEBUG_INVALID_MEMORY_ADDRESS se qualquer parte da memória solicitada foi ilegível.|  
|`None`|Indica que o chamador deseja o comportamento padrão para ReadMemory.|  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Referência de interfaces de script do Windows](../../winscript/reference/windows-script-interfaces-reference.md)