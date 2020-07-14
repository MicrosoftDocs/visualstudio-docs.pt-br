---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8fe7ced486524c7409532e140f48f841b5e55078
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467641"
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

## <a name="see-also"></a>Veja também
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)