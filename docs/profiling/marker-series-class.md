---
description: Representa um canal serial de eventos gerados por um único provedor.
title: Classe marker_series | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_series
helpviewer_keywords:
- Concurrency, diagnostic::marker_series class
ms.assetid: b8445ed0-c512-4f92-b6b4-3d05c044f939
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4df579ff4eb43dfca4c386716c49f12dae04e9fa
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223609"
---
# <a name="marker_series-class"></a>Classe marker_series
Representa um canal serial de eventos gerados por um único provedor.

## <a name="syntax"></a>Sintaxe

```cpp
class marker_series;
```

## <a name="members"></a>Membros

### <a name="public-constructors"></a>Construtores públicos

|Name|Descrição|
|----------|-----------------|
|[Construtor marker_series:: marker_series](../profiling/marker-series-marker-series-constructor.md)|Inicializa uma nova instância da classe `marker_series`.|
|[destruidor de marker_series:: ~ marker_series](../profiling/marker-series-tilde-marker-series-destructor.md)|Destrói o objeto marker_series e libera todos os recursos alocados.|

### <a name="public-methods"></a>Métodos públicos

|Name|Descrição|
|----------|-----------------|
|[método marker_series:: is_enabled](../profiling/marker-series-is-enabled-method.md)|Determina se alguma sessão habilitou o provedor.|
|[método marker_series:: write_alert](../profiling/marker-series-write-alert-method.md)|Grava um alerta para o arquivo de rastreamento da Visualização Simultânea.|
|[método marker_series:: write_flag](../profiling/marker-series-write-flag-method.md)|Grava um sinalizador para o arquivo de rastreamento da Visualização Simultânea.|
|[método marker_series:: write_message](../profiling/marker-series-write-message-method.md)|Grava uma mensagem para o arquivo de rastreamento da Visualização Simultânea.|

## <a name="inheritance-hierarchy"></a>Hierarquia de herança
 `marker_series`

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkersobj.h*

 **Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Confira também
- [namespace de diagnóstico](../profiling/diagnostic-namespace.md)
