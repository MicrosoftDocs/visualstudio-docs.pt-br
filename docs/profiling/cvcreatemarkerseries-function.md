---
title: Função CvCreateMarkerSeries | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvCreateMarkerSeriesA
- cvmarkers/CvCreateMarkerSeriesW
helpviewer_keywords:
- CvCreateMarkerSeriesA method
- CvCreateMarkerSeriesW method
ms.assetid: e280530b-137a-43a7-8643-aa514ab86ed7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fc44e9e1a9a1d17d3f5b0f31515e2402e9512c55
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332205"
---
# <a name="cvcreatemarkerseries-function"></a>Função CvCreateMarkerSeries
Cria a série de marcador para determinado provedor.

## <a name="syntax"></a>Sintaxe

```C
_Check_return_ HRESULT CvCreateMarkerSeriesW(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCWSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);

_Check_return_ HRESULT CvCreateMarkerSeriesA(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);
```

#### <a name="parameters"></a>Parâmetros
 `pProvider` Objeto do provedor inicializado anteriormente por CvInitProvider. Não pode ser NULL.

 `pSeriesName` Nome da série de marcador. Não pode ser NULL, mas uma cadeia de caracteres vazia é permitida.

 `ppMarkerSeries` Endereço de uma variável de saída que armazenará o contexto de série de marcador. Não pode ser NULL.

## <a name="return-value"></a>Valor retornado
 S_OK quando a série de marcador é criada com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

 **Unicode:** CvCreateMarkerSeriesW

 **ANSI:** CvCreateMarkerSeriesA

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)