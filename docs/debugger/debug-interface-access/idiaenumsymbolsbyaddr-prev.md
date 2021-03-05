---
description: Recupera os símbolos anteriores no endereço de ordenação.
title: IDiaEnumSymbolsByAddr::Prev | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Prev method
ms.assetid: da3b3dca-68cb-4cb0-b25c-e28a1ffe49d3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 721eaf80e0bd7121d9e8286315b63422edbb745d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148636"
---
# <a name="idiaenumsymbolsbyaddrprev"></a>IDiaEnumSymbolsByAddr::Prev
Recupera os símbolos anteriores no endereço de ordenação.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Prev ( 
   ULONG        celt,
   IDiaSymbol** rgelt,
   ULONG*       pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de símbolos no enumerador a ser recuperado.

 rgelt

fora Uma matriz que deve ser preenchida com objetos [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representam os símbolos desejados.

 pceltFetched

fora Retorna o número de símbolos no enumerador obtido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver símbolos anteriores. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Esse método atualiza a posição do enumerador pelo número de elementos buscados.

## <a name="see-also"></a>Confira também
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
