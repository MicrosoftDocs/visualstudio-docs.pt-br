---
title: Método marker_series::write_flag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersojb/Concurrency, diagnostic::marker_series::write_flag
helpviewer_keywords:
- Concurrency, diagnostic::marker_series::write_flag method
ms.assetid: ca07f388-e5d5-46fd-b991-fe6e9029a68f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: edd141f6b99dc3836d99ebdbc4aab9af7150e4ff
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329227"
---
# <a name="marker_serieswrite_flag-method"></a>Método marker_series::write_flag
Grava um sinalizador para o arquivo de rastreamento da Visualização Simultânea.

## <a name="syntax"></a>Sintaxe

```cpp
void write_flag(
   _In_ LPCTSTR _Format,
   ...
);
void write_flag(
   marker_importance _Importance,
   _In_ LPCTSTR _Format,
   ...
);
void write_flag(
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
void write_flag(
   marker_importance _Importance,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>Parâmetros
 `_Format` Uma cadeia de caracteres de formato composto, que contém um texto intercalado com zero ou mais itens de formato correspondentes aos objetos na lista de argumentos.

 `_Importance` Nível de prioridade.

 `_Category` Categoria.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Veja também
- [classe marker_series](../profiling/marker-series-class.md)