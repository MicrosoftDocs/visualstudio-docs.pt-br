---
title: Enumeração PROFILER_HEAP_ENUM_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 17936b7a-40d5-4774-b92b-b24ee391591e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f2a7a27f4d9d7f834b07a2db5ba8433b63222a3b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734106"
---
# <a name="profilerheapenumflags-enumeration"></a>Enumeração PROFILER_HEAP_ENUM_FLAGS
Sinalizadores que representam se apontada informações extras sobre um objeto do heap em uma relação de objeto são expostos. Usado no [EnumHeap2](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef [v1_enum] enum {    PROFILER_HEAP_ENUM_FLAGS_NONE                      = 0x00000000,    PROFILER_HEAP_ENUM_FLAGS_STORE_RELATIONSHIP_FLAGS  = 0x00000001,} PROFILER_HEAP_ENUM_FLAGS;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Valor|Descrição|  
|------------|-----------|-----------------|  
|PROFILER_HEAP_ENUM_FLAGS_NONE|0x00000000|Este objeto do heap não expõe informações adicionais sobre uma relação de objeto. Esse objeto heap se comporta da mesma maneira como [IActiveScriptProfilerControl3::HeapEnum](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md).|  
|PROFILER_HEAP_ENUM_ENUM_ STORE_RELATIONSHIP_FLAGS|0x00000001|Esse objeto heap irá expor informações sobre se um objeto apontado em uma relação de objeto é um método getter ou setter. Essas informações serão armazenadas em alta 2 bytes (16 bits) da [PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo](../../winscript/reference/profiler-heap-object-relationship-structure.md) campo como uma da [PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS](../../winscript/reference/profiler-heap-object-relationship-flags-enumeration.md) valores de enumeração.|  
|PROFILER_HEAP_ENUM_FLAGS_SUBSTRINGS|0x00000002|Esse objeto heap é usado para exibir a subcadeia de caracteres corretamente.|  
|PROFILER_HEAP_ENUM_FLAGS_RELATIONSHIP_SUBSTRINGS|PROFILER_HEAP_ENUM_FLAGS_STORE_RELATIONSHIP_FLAGS &#124; PROFILER_HEAP_ENUM_FLAGS_SUBSTRINGS|Esse objeto heap é usado para exibir a subcadeia de caracteres corretamente.|