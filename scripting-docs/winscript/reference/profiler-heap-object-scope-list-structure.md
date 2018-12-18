---
title: Estrutura PROFILER_HEAP_OBJECT_SCOPE_LIST | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 33ebaa31-0a35-47d5-a4e3-afd83e16f53e
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 67f0972faee11e15bd5d0e9a219e439df49d9672
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734256"
---
# <a name="profilerheapobjectscopelist-structure"></a>Estrutura PROFILER_HEAP_OBJECT_SCOPE_LIST
Essa estrutura é associada a somente os objetos de função. A lista de escopo representa o fechamento da função como uma lista de escopos, onde cada escopo é um objeto de heap com uma lista de propriedades associado que representa as variáveis em cada escopo fornecido. Em alguns casos, os nomes de objetos em que o escopo não fiquem disponível e somente seu índice na lista de propriedades está disponível.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef struct _PROFILER_HEAP_OBJECT_SCOPE_LIST{    UINT count;    [size_is(count)] PROFILER_HEAP_OBJECT_ID scopes[];} PROFILER_HEAP_OBJECT_SCOPE_LIST;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Tipo|Descrição|  
|------------|----------|-----------------|  
|count|UINT|O número de escopos|  
|escopos|[Tipo PROFILER_HEAP_OBJECT_ID](../../winscript/reference/profiler-heap-object-id-type.md)|Uma matriz de escopos.|