---
title: Interface IActiveScriptProfilerHeapEnum | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 16756d0e-547a-4825-8b7b-a7e0e4708a04
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4761e8c7d4cc9c3372c7906e1503b8dbd059ca33
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724706"
---
# <a name="iactivescriptprofilerheapenum-interface"></a>Interface IActiveScriptProfilerHeapEnum
Os objetos de um iterador sobre o heap associada com um mecanismo de script, coletado pelo [IActiveScriptProfilerControl3::EnumHeap método](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
interface IActiveScriptProfilerHeapEnum : IUnknown  
```  
  
## <a name="methods"></a>Métodos  
 [Método IActiveScriptProfilerHeapEnum::Next](../../winscript/reference/iactivescriptprofilerheapenum-next-method.md)  
 Obtém o próximo objeto ou objetos no conjunto de objetos do heap coletados pelo [IActiveScriptProfilerControl3::EnumHeap método](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md).  
  
 [Método IActiveScriptProfilerHeapEnum::GetOptionalInfo](../../winscript/reference/iactivescriptprofilerheapenum-getoptionalinfo-method.md)  
 Obtém informações opcionais no objeto especificado no conjunto de objetos do heap coletados pelo [IActiveScriptProfilerControl3::EnumHeap método](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md).  
  
 [Método IActiveScriptProfilerHeapEnum::FreeObjectAndOptionalInfo](../../winscript/reference/iactivescriptprofilerheapenum-freeobjectandoptionalinfo-method.md)  
 Libera especificado [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md) estruturas e seus respectivos [estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md) elementos.  
  
 [IActiveScriptProfilerHeapEnum::GetNameIdMap](../../winscript/reference/iactivescriptprofilerheapenum-getnameidmap.md)  
 Retorna os nomes de cadeia de caracteres correspondente ao [tipo PROFILER_HEAP_OBJECT_NAME_ID](../../winscript/reference/profiler-heap-object-name-id-type.md) valores.