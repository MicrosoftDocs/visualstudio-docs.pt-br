---
title: Função CvReleaseProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseProvider
helpviewer_keywords:
- CvReleaseProvider method
ms.assetid: 8d74379e-295d-452b-bd5f-0769df387d4f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0347d3e2345defb13a67e0e0d730e010be618a21
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332179"
---
# <a name="cvreleaseprovider-function"></a>Função CvReleaseProvider
Libera o provedor de marcador. A liberação do provedor de marcador não afetará a série de marcador criada anteriormente desse provedor. A série de marcador deve ser liberada separadamente pela chamada CvReleaseMarkerSeries. A falha ao liberar o provedor causa uma perda de memória.

## <a name="syntax"></a>Sintaxe

```C
HRESULT CvReleaseProvider(
   _In_ PCV_PROVIDER pProvider
);
```

#### <a name="parameters"></a>Parâmetros
 `pProvider` Contexto do provedor. Não pode ser NULL.

## <a name="return-value"></a>Valor Retornado
 S_OK quando o provedor é liberado com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)