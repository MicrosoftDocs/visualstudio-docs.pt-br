---
description: Representa o nível de importância de um marcador da Visualização Simultânea.
title: Enumeração de marker_importance | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_importance
helpviewer_keywords:
- Concurrency, diagnostic::marker_importance enumeration
ms.assetid: d5524ea0-0227-4d8e-9122-332291042df5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2c2e7560c91882afe1ee2608bb2ae2fc105738dc
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223934"
---
# <a name="marker_importance-enumeration"></a>Enumeração marker_importance
Representa o nível de importância de um marcador da Visualização Simultânea.

## <a name="syntax"></a>Sintaxe

```cpp
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
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Confira também
- [namespace de diagnóstico](../profiling/diagnostic-namespace.md)
