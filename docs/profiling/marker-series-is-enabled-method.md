---
title: Método marker_series::is_enabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_series::is_enabled
helpviewer_keywords:
- Concurrency, diagnostic::marker_series::is_enabled method
ms.assetid: 8ce4dd50-ca29-4c72-98d6-582693f7d501
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ff6b0449c877b5ae925ba2088917d7bacab4c34
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330669"
---
# <a name="marker_seriesis_enabled-method"></a>Método marker_series::is_enabled
Determina se alguma sessão habilitou o provedor.

## <a name="syntax"></a>Sintaxe

```cpp
bool is_enabled();
bool is_enabled(
   marker_importance _Importance,
   int _Category
);
```

#### <a name="parameters"></a>Parâmetros
 `_Importance` Nível de prioridade.

 `_Category` Categoria.

## <a name="return-value"></a>Valor retornado

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Veja também
- [classe marker_series](../profiling/marker-series-class.md)