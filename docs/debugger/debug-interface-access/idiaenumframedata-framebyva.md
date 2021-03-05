---
description: Retorna um quadro por endereço virtual (VA).
title: IDiaEnumFrameData::frameByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByVA method
ms.assetid: 0b1e441b-710a-46d8-8060-bed39071c834
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2fa167749574165df2a7acffdc232e3fd4c66e4a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158074"
---
# <a name="idiaenumframedataframebyva"></a>IDiaEnumFrameData::frameByVA
Retorna um quadro por endereço virtual (VA).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT frameByVA( 
   ULONGLONG       virtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>Parâmetros
 virtualAddress

no VA do quadro de interesse.

 frame

fora Retorna um objeto [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) que representa o quadro que contém o endereço fornecido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se nenhum dado de quadro corresponder ao endereço especificado. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
