---
title: Estrutura PROFILER_PROPERTY_TYPE_SUBSTRING_INFO | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3845c872-4302-47b6-8912-7b2d7a3b3357
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 5f873cdf2ebd394e48c1513135f1acdcd700c283
ms.sourcegitcommit: 8bf9e51c77a5a602fab9513b9187e59e57dfebad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54345637"
---
# <a name="profilerpropertytypesubstringinfo-structure"></a>Estrutura PROFILER_PROPERTY_TYPE_SUBSTRING_INFO
Representa informações sobre o tipo de subcadeia de caracteres usada na relação. Usado na [estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef struct _PROFILER_PROPERTY_TYPE_SUBSTRING_INFO {    UINT length;    LPCWSTR value; } PROFILER_PROPERTY_TYPE_SUBSTRING_INFO;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Tipo|Descrição|  
|------------|----------|-----------------|  
|length|UINT|O objeto é UINT.|  
|Valor |LPCWSTR|O objeto é um LPCWSTR.|