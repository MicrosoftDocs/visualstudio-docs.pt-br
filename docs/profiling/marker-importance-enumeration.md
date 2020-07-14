---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d67a1806034d55147379626b6eb4f868532e4d77
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330737"
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

## <a name="see-also"></a>Veja também
- [namespace de diagnóstico](../profiling/diagnostic-namespace.md)