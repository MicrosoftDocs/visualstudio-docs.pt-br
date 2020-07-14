---
title: Método marker_series::write_alert | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic:marker_series::write_alert
helpviewer_keywords:
- Concurrency, diagnostic:marker_series::write_alert method
ms.assetid: 9d5465c7-f862-47a7-b249-4116605075a6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d5e79bab25885c8759ea5726b037771a4943c563
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329635"
---
# <a name="marker_serieswrite_alert-method"></a>Método marker_series::write_alert
Grava um alerta para o arquivo de rastreamento da Visualização Simultânea.

## <a name="syntax"></a>Sintaxe

```cpp
void write_alert(
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>Parâmetros
 `_Format` Uma cadeia de caracteres de formato composto, que contém um texto intercalado com zero ou mais itens de formato correspondentes aos objetos na lista de argumentos.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Veja também
- [classe marker_series](../profiling/marker-series-class.md)