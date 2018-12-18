---
title: Script ativo Profiler constantes, enumerações e estruturas | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6e079d84-9dde-46fc-8a6a-18e902f60ecc
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a37f64b14d0d732e48de66bb5268d47c95426937
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24642046"
---
# <a name="active-script-profiler-constants-enumerations-and-structures"></a>Constantes, enumerações e estruturas de criador de perfil do script ativo
As enumerações a seguir são usadas por Active Interfaces do criador de perfil de Script.  
  
## <a name="constants-enumerations-and-structures"></a>Constantes, Enumerações e Estruturas  
  
|Constantes|Descrição|  
|---------------|-----------------|  
|[Tipo PROFILER_EXTERNAL_OBJECT_ADDRESS](../../winscript/reference/profiler-external-object-address-type.md)|O endereço externo do objeto do criador de perfil. Usado em [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md) e [estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md).|  
|[Tipo PROFILER_HEAP_OBJECT_ID](../../winscript/reference/profiler-heap-object-id-type.md)|A ID do objeto heap. Usado em [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md)[estrutura PROFILER_HEAP_OBJECT_SCOPE_LIST](../../winscript/reference/profiler-heap-object-scope-list-structure.md), [estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md)e [Estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md).|  
|[Tipo PROFILER_HEAP_OBJECT_NAME_ID](../../winscript/reference/profiler-heap-object-name-id-type.md)|A ID do nome do objeto heap. Usado em [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md).|  
  
|Enumerações|Descrição|  
|------------------|-----------------|  
|[Enumeração PROFILER_EVENT_MASK](../../winscript/reference/profiler-event-mask-enumeration.md)|Indica os tipos de eventos que devem ser analisados.|  
|[Enumeração PROFILER_HEAP_ENUM_FLAGS](../../winscript/reference/profiler-heap-enum-flags-enumeration.md)|Sinalizadores que representam se apontada informações extras sobre um objeto do heap em uma relação de objeto são expostos. Usado no [IActiveScriptProfilerControl5::EnumHeap2 método](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md).|  
|[Enumeração PROFILER_HEAP_OBJECT_FLAGS](../../winscript/reference/profiler-heap-object-flags-enumeration.md)|Sinalizadores que representam informações básicas sobre o objeto do heap. Usado no [estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md).|  
|[Enumeração PROFILER_HEAP_OBJECT_OPTIONAL_INFO_TYPE](../../winscript/reference/profiler-heap-object-optional-info-type-enumeration.md)|Representa os tipos diferentes de informações opcionais. Usado em [estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md).|  
|[Enumeração PROFILER_RELATIONSHIP_INFO](../../winscript/reference/profiler-relationship-info-enumeration.md)|Representa informações sobre o objeto da relação. Usado em [estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md).|  
|[Enumeração PROFILER_SCRIPT_TYPE](../../winscript/reference/profiler-script-type-enumeration.md)|Especifica o tipo de script.|  
  
|Estruturas|Descrição|  
|----------------|-----------------|  
|[Estrutura PROFILER_HEAP_OBJECT](../../winscript/reference/profiler-heap-object-structure.md)|Representa os objetos do heap coletados por [IActiveScriptProfilerControl3::EnumHeap método](../../winscript/reference/iactivescriptprofilercontrol3-enumheap-method.md).|  
|[Estrutura PROFILER_HEAP_OBJECT_OPTIONAL_INFO](../../winscript/reference/profiler-heap-object-optional-info-structure.md)|Representa informações opcionais sobre objetos do heap.|  
|[Estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md)|Representa uma relação de um objeto do heap.|  
|[Estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP_LIST](../../winscript/reference/profiler-heap-object-relationship-list-structure.md)|Representa uma lista de relações que pertencem a um objeto do heap.|  
|[Estrutura PROFILER_HEAP_OBJECT_SCOPE_LIST](../../winscript/reference/profiler-heap-object-scope-list-structure.md)|Essa estrutura é associada a somente os objetos de função. A lista de escopo representa o fechamento da função como uma lista de escopos, onde cada escopo é um objeto de heap com uma lista de propriedades associado que representa as variáveis em cada escopo fornecido. Em alguns casos, os nomes de objetos no escopo podem não estar disponíveis, somente suas ids.|  
|[Estrutura PROFILER_PROPERTY_TYPE_SUBSTRING_INFO](../../winscript/reference/profiler-property-type-substring-info-structure.md)|Representa informações sobre o tipo da subcadeia de caracteres.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces do criador de perfil de script ativo](../../winscript/reference/active-script-profiler-interfaces.md)