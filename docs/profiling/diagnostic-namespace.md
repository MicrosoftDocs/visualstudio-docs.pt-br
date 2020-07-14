---
title: Namespace diagnostic | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic
helpviewer_keywords:
- Concurrency, diagnostic namespace
ms.assetid: ad786b19-7c4c-46ee-bfb6-c4752b373a09
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 680d304a8e4d21365d82f654265ae2f34582b636
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330253"
---
# <a name="diagnostic-namespace"></a>Namespace de diagnóstico
O namespace `diagnostics` fornece funcionalidade para emitir marcadores de Visualização Simultânea.

## <a name="syntax"></a>Sintaxe

```cpp
namespace diagnostic;
```

## <a name="members"></a>Membros

### <a name="classes"></a>Classes

|Nome|Descrição|
|----------|-----------------|
|[Classe marker_series](../profiling/marker-series-class.md)|Representa um canal serial de eventos gerados por um único provedor.|
|[Classe span](../profiling/span-class.md)|Define uma fase do aplicativo.|

### <a name="enumerations"></a>Enumerações

|Nome|Descrição|
|----------|-----------------|
|[Enumeração marker_importance](../profiling/marker-importance-enumeration.md)|Representa o nível de importância de um marcador da Visualização Simultânea.|

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Simultaneidade

## <a name="see-also"></a>Veja também
- [Namespace de simultaneidade (Visualizador de simultaneidade)](../profiling/concurrency-namespace-concurrency-visualizer.md)