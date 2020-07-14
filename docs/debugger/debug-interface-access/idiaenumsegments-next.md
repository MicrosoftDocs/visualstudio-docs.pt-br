---
title: IDiaEnumSegments::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8e87efa1ed616a38ccb79fec1e286417c10124b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468026"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
Recupera um número especificado de segmentos na sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next ( 
   ULONG         celt,
   IDiaSegment** rgelt,
   ULONG*        pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de segmentos no enumerador a ser recuperado.

 rgelt

fora Uma matriz que deve ser preenchida com os objetos [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) desejados que representam os segmentos.

 pceltFetched

fora Retorna o número de segmentos no enumerador obtido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais segmentos. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)