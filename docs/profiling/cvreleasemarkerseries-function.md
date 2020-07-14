---
title: Função CvReleaseMarkerSeries | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseMarkerSeries
helpviewer_keywords:
- CvReleaseMarkerSeries method
ms.assetid: 3b4711ee-e534-411d-9128-f69cd7932a48
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 84db5dac77fbbc51c9f1c0e24173dcc8ca1d68c1
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332195"
---
# <a name="cvreleasemarkerseries-function"></a>Função CvReleaseMarkerSeries
Libera a série de marcador. Não use um objeto de série de marcador após a liberação; caso contrário, o aplicativo poderá falhar. A falha ao liberar a série de marcador causa uma perda de memória.

## <a name="syntax"></a>Sintaxe

```C
HRESULT CvReleaseMarkerSeries(
   _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries
);
```

#### <a name="parameters"></a>Parâmetros
 `pMarkerSeries` Endereço da variável de objeto do provedor. O endereço não pode ser NULL; a variável pode ter qualquer valor.

## <a name="return-value"></a>Valor Retornado
 S_OK quando a série de marcador é liberada com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)