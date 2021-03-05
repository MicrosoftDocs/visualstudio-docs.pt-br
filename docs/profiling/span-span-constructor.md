---
description: Inicializa uma nova instância da classe span.
title: Construtor span::span | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span::span
helpviewer_keywords:
- Concurrency::diagnostic::span constructor
ms.assetid: 8b5578aa-5e5c-4ac7-87c7-ce87c4246e2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fdffdc59b31f5f04817536769d9a712484e6cdd7
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223856"
---
# <a name="spanspan-constructor"></a>Construtor span::span

Inicializa uma nova instância da classe `span`.

## <a name="syntax"></a>Sintaxe

```cpp
span(
   const marker_series& _Series,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>Parâmetros

`_Series` Contexto de série de marcador válido.

`_Format` Uma cadeia de caracteres de formato composto, que contém um texto intercalado com zero ou mais itens de formato correspondentes aos objetos na lista de argumentos.

`_Importance` Nível de prioridade.

`_Category` Categoria.

## <a name="requirements"></a>Requisitos

**Cabeçalho:** *cvmarkersobj.h*

**Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Confira também

- [classe span](../profiling/span-class.md)
