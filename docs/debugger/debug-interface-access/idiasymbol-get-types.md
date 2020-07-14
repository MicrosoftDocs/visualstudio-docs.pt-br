---
title: IDiaSymbol::get_types | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d947eed08ba28cfdd68e2cd7d34998412fc8bc3a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461681"
---
# <a name="idiasymbolget_types"></a>IDiaSymbol::get_types
Recupera uma matriz de tipos específicos do compilador para este símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_types ( 
   DWORD       cTypes,
   DWORD*      pcTypes,
   IDiaSymbol* types[]
);
```

#### <a name="parameters"></a>Parâmetros
 `cTypes`

no Tamanho do buffer para armazenar os dados.

 `pcTypes`

fora Retorna o número de tipos gravados ou, se o `types` parâmetro for `NULL` , o número total de tipos disponíveis.

 `types[]`

fora Uma matriz que deve ser preenchida com os objetos [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representam todos os tipos desse símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)