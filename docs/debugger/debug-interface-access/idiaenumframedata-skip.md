---
description: Ignora um número especificado de elementos de dados de quadro em uma sequência de enumeração.
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e2fe993c524a846545a13ab14787c9c6fd5c92e0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158025"
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

## <a name="see-also"></a>Confira também
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
