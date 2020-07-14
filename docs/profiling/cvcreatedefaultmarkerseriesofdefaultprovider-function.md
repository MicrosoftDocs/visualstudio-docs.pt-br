---
title: Função CvCreateDefaultMarkerSeriesOfDefaultProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvCreateDefaultMarkerSeriesOfDefaultProvider
helpviewer_keywords:
- CvCreateDefaultMarkerSeriesOfDefaultProvider method
ms.assetid: 24eb80f8-8fca-4c47-93b5-bb1eb8ffdffd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 560ecc3d66dc2bc84d2ef301654b392aee6a42b4
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332218"
---
# <a name="cvcreatedefaultmarkerseriesofdefaultprovider-function"></a>Função CvCreateDefaultMarkerSeriesOfDefaultProvider
Cria a série de marcador padrão de um provedor padrão.

## <a name="syntax"></a>Sintaxe

```C
HRESULT CvCreateDefaultMarkerSeriesOfDefaultProvider(
   _Out_ PCV_PROVIDER* ppProvider,
   _Out_ PCV_MARKERSERIES* ppMarkerSeries
);
```

#### <a name="parameters"></a>Parâmetros
 `ppProvider` Endereço da variável de objeto do provedor. O endereço não pode ser NULL; a variável pode ter qualquer valor.

 `ppMarkerSeries` Endereço da variável de objeto de série de marcador. O endereço não pode ser NULL; a variável pode ter qualquer valor.

## <a name="return-value"></a>Valor retornado
 S_OK quando o provedor e a série de marcador são criados com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)