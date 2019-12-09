---
title: Construtor span::span | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span::span
helpviewer_keywords:
- Concurrency::diagnostic::span constructor
ms.assetid: 8b5578aa-5e5c-4ac7-87c7-ce87c4246e2c
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df6df731de90a9aad9e6cc637b3f218e481b66b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198293"
---
# <a name="spanspan-constructor"></a>Construtor span::span

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Inicializa uma nova instância da classe `span`.

## <a name="syntax"></a>Sintaxe

```
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

**Cabeçalho:** cvmarkersobj.h

**Namespace:** Concurrency::diagnostic

## <a name="see-also"></a>Veja também

[Classe span](../profiling/span-class.md)
