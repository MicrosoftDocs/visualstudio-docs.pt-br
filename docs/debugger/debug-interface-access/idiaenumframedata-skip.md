---
title: IDiaEnumFrameData::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Skip method
ms.assetid: 67140b4c-7125-4895-932d-42412326da29
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 02c56c0b49844b72384d641a53eb513c2a504acb
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468304"
---
# <a name="idiaenumframedataskip"></a>IDiaEnumFrameData::Skip
Ignora um número especificado de elementos de dados de quadro em uma sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de elementos de dados de quadro na sequência de enumeração a serem ignorados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK` ; caso contrário, retornará `S_FALSE` se não houver mais registros a serem ignorados.

## <a name="see-also"></a>Veja também
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)