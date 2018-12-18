---
title: 'Método: Getoptionalinfo | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 99ed9df5-71cf-4c25-b189-af9accc466ee
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6ad237f2feb173408e895984dab7e7455004d16
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724676"
---
# <a name="iactivescriptprofilerheapenumgetoptionalinfo-method"></a>Método IActiveScriptProfilerHeapEnum::GetOptionalInfo
Obtém informações opcionais no objeto especificado (do conjunto de objetos do heap retornados do [IActiveScriptProfilerControl3::EnumHeap método](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md)).  
  
 Você não deve liberar a memória retornada com os objetos retornados. Em vez disso, você deve chamar o [: Freeobjectandoptionalinfo método](../../winscript/reference/iactivescriptprofilerheapenum-freeobjectandoptionalinfo-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetOptionalInfo (    [in] PROFILER_HEAP_OBJECT* heapObject,    [in] ULONG celt,    [out, size_is(celt)] PROFILER_HEAP_OBJECT_OPTIONAL_INFO* optionalInfo);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `heapObject`  
 O [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md) para o qual retornar as informações.  
  
 `celt`  
 O número de [estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md) estruturas para retornar.  
  
 `optionalInfo`  
 [out] Uma matriz de [estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md) estruturas para o objeto especificado.  
  
## <a name="return-value"></a>Valor de retorno  
 O HRESULT.