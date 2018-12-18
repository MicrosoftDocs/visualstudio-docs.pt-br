---
title: Enumeração PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1a41b642-c9a9-4d83-b943-d59b232eebf6
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ab542225e0238dbd40f90d9de66d43d0791e05e0
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734006"
---
# <a name="profilerheapobjectrelationshipflags-enumeration"></a>Enumeração PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS
Sinalizadores que representam se um objeto de heap apontada em uma relação de objeto é um método getter ou setter. Usado no [EnumHeap2](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md) método quando o valor PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS é especificado no `enumFlags` parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef [v1_enum] enum {    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_NONE                      = 0x00000000,    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_GET_ACCESSOR           = 0x00010000,    PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_SET_ACCESSOR           = 0x00020000,} PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Valor|Descrição|  
|------------|-----------|-----------------|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_NONE|0x00000000|Esse objeto heap apontado em uma relação de objeto não for identificado como método um getter ou setter.|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_GET_ACCESSOR|0x00010000|O objeto de heap apontado em uma relação de objeto é um método getter. Essas informações serão armazenadas em alta 2 bytes (16 bits) da [PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo](../../winscript/reference/profiler-heap-object-relationship-structure.md) campo.|  
|PROFILER_HEAP_OBJECT_RELATIONSHIP_FLAGS_IS_SET_ACCESSOR|0x00020000|O objeto de heap apontado em uma relação de objeto é um método de setter. Essas informações serão armazenadas em alta 2 bytes (16 bits) da `PROFILER_HEAP_OBJECT_RELATIONSHIP.relationshipInfo` campo.|