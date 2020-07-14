---
title: IDiaEnumSymbolsByAddr::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Next method
ms.assetid: a1320587-7ce7-401f-9548-2f8bcece5cc3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2a4be91f2439c198ca7424ba13542c68d41c6b7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467662"
---
# <a name="idiaenumsymbolsbyaddrnext"></a>IDiaEnumSymbolsByAddr::Next
Recupera os próximos símbolos no endereço de ordenação.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next ( 
   ULONG        celt,
   IDiaSymbol** rgelt,
   ULONG*       pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de símbolos no enumerador a ser recuperado.

 rgelt

fora Uma matriz que deve ser preenchida com o objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa os símbolos desejados.

 pceltFetched

fora Retorna o número de símbolos no enumerador obtido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais símbolos. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Esse método atualiza a posição do enumerador pelo número de elementos buscados.

## <a name="see-also"></a>Veja também
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)