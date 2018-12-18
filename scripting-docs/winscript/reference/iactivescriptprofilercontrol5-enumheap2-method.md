---
title: Método IActiveScriptProfilerControl5::EnumHeap2 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a25859eb-ac28-4a97-bcb3-33788982a76b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c493acdb2843877c506d9d84e145a79ac2d60d7
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724656"
---
# <a name="iactivescriptprofilercontrol5enumheap2-method"></a>Método IActiveScriptProfilerControl5::EnumHeap2
Retorna uma interface ([IActiveScriptProfilerHeapEnum Interface](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)) que pode ser usado para iterar sobre os objetos do heap de GC no contexto do mecanismo de script associados.  
  
 Você pode chamar este método ou depuração ou modo de liberação. Esse método deve ser chamado quando o thread de interface do usuário está ocioso. Depois que o método é chamado, nenhuma operação deve ser executada contra o mecanismo de script exceto [método Iactivescriptprofilerheapenum:](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md) até [método Iactivescriptprofilerheapenum:](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)retornará S_FALSE ou [IActiveScriptProfilerHeapEnum Interface](../../winscript/reference/iactivescriptprofilerheapenum-interface.md) ponteiro de interface é liberado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT EnumHeap2(    [in] PROFILER_HEAP_ENUM_FLAGS enumFlags,    [out] IActiveScriptProfilerHeapEnum** ppEnum);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 enumFlags  
 Valor que especifica se as informações extras sobre um objeto apontado em uma relação de objeto é exposto. Informações extras podem indicar se o objeto apontado é um método getter ou setter. Para obter mais informações, consulte [enumeração PROFILER_HEAP_ENUM_FLAGS](../../winscript/reference/profiler-heap-enum-flags-enumeration.md).  
  
 ppEnum  
 [out] Retorna o [Interface IActiveScriptProfilerHeapEnum](../../winscript/reference/iactivescriptprofilerheapenum-interface.md).  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um HRESULT. Os valores possíveis são:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|A enumeração de heap foi concluída com êxito.|  
|`E_OUTOFMEMORY`|Não havia memória suficiente executar a enumeração de heap.|  
|`E_FAIL`|Ocorreu um erro interno.|