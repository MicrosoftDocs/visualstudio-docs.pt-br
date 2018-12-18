---
title: Enumeração de marker_importance | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_importance
helpviewer_keywords:
- Concurrency::diagnostic::marker_importance enumeration
ms.assetid: d5524ea0-0227-4d8e-9122-332291042df5
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 32e57a9463e6c6966c215066fd470b62596f5481
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756852"
---
# <a name="markerimportance-enumeration"></a>Enumeração marker_importance
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Representa o nível de importância de um marcador da Visualização Simultânea.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
enum marker_importance;  
```  
  
## <a name="members"></a>Membros  
  
### <a name="values"></a>Valores  
  
|Nome|Descrição|  
|----------|-----------------|  
|`critical_importance`|Especifica que o marcador tem importância crítica.|  
|`high_importance`|Especifica que o marcador tem alta importância.|  
|`low_importance`|Especifica que o marcador tem baixa importância.|  
|`normal_importance`|Especifica que o marcador tem importância normal.|  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** cvmarkersobj.h  
  
 **Namespace:** Concurrency::diagnostic  
  
## <a name="see-also"></a>Consulte também  
 [Namespace de diagnóstico](../profiling/diagnostic-namespace.md)



