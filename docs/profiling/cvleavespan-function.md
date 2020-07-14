---
title: Função CvLeaveSpan | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvLeaveSpan
helpviewer_keywords:
- CvLeaveSpan method
ms.assetid: 3bf65fdf-a471-4efd-ac7a-03e701bbae5d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 113d6aafbd09f6b726613405a8c1eb82f9e202e5
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330033"
---
# <a name="cvleavespan-function"></a>Função CvLeaveSpan
Marca o fim do intervalo.

## <a name="syntax"></a>Sintaxe

```C
HRESULT CvLeaveSpan(
   _In_ PCV_SPAN pSpan
);
```

#### <a name="parameters"></a>Parâmetros
 `pSpan` Objeto de período retornado pela chamada anterior a CvEnterSpan*. Não pode ser NULL.

## <a name="return-value"></a>Valor Retornado
 S_OK quando a mensagem é gravada com êxito. Código de erro em caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)