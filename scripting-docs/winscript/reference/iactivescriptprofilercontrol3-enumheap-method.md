---
title: Método IActiveScriptProfilerControl3::EnumHeap | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2799d06d-20dd-4c12-9646-554c0ea3606e
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7d6fc79a9d6d35e35181c3505e07af2d9a1962c2
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724556"
---
# <a name="iactivescriptprofilercontrol3enumheap-method"></a>Método IActiveScriptProfilerControl3::EnumHeap
Retorna uma interface ([IActiveScriptProfilerHeapEnum Interface](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)) que pode ser usado para iterar sobre os objetos do heap de GC no contexto do mecanismo de script associados.  
  
 Você pode chamar este método ou depuração ou modo de liberação. Esse método deve ser chamado quando o thread de interface do usuário está ocioso. Depois que o método é chamado, nenhuma operação deve ser executada contra o mecanismo de script exceto [método Iactivescriptprofilerheapenum:](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md) até [método Iactivescriptprofilerheapenum:](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)retornará S_FALSE ou [IActiveScriptProfilerHeapEnum Interface](../../winscript/reference/iactivescriptprofilerheapenum-interface.md) ponteiro de interface é liberado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT EnumHeap([out] IActiveScriptProfilerHeapEnum** ppEnum);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 ppEnum  
 [out] Retorna o [Interface IActiveScriptProfilerHeapEnum](../../winscript/reference/iactivescriptprofilerheapenum-interface.md).  
  
## <a name="return-value"></a>Valor de retorno  
 O HRESULT.