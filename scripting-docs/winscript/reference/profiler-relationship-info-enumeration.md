---
title: Enumeração PROFILER_RELATIONSHIP_INFO | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: fae69317-6224-4a6a-8e9e-ccaa6a330818
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f01ca5e001d45907af70b46b6dc362e8ae0b2044
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733926"
---
# <a name="profilerrelationshipinfo-enumeration"></a>Enumeração PROFILER_RELATIONSHIP_INFO
Representa informações sobre o objeto da relação. Usado em [estrutura PROFILER_HEAP_OBJECT_RELATIONSHIP](../../winscript/reference/profiler-heap-object-relationship-structure.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef [v1_enum] enum {    PROFILER_PROPERTY_TYPE_NUMBER = 0x01,    PROFILER_PROPERTY_TYPE_STRING = 0x02,    PROFILER_PROPERTY_TYPE_HEAP_OBJECT = 0x03,    PROFILER_PROPERTY_TYPE_EXTERNAL_OBJECT = 0x04,    PROFILER_PROPERTY_TYPE_BSTR = 0x05,} PROFILER_RELATIONSHIP_INFO;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Valor|Descrição|  
|------------|-----------|-----------------|  
|PROFILER_PROPERTY_TYPE_NUMBER|0x01|O objeto é um número.|  
|PROFILER_PROPERTY_TYPE_STRING|0x02|O objeto é uma cadeia de caracteres.|  
|PROFILER_PROPERTY_TYPE_HEAP_OBJECT|0x03|O objeto é um heap.|  
|PROFILER_PROPERTY_TYPE_EXTERNAL_OBJECT|0x04|O objeto é externo, ou seja, não no heap de coleta de lixo.|  
|PROFILER_PROPERTY_TYPE_BSTR|0x05|O objeto é um BSTR.|  
|PROFILER_PROPERTY_TYPE_SUBSTRING|0x06|O objeto é uma subcadeia de caracteres.|