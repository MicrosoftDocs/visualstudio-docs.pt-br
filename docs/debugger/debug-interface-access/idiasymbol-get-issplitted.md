---
description: Recupera um sinalizador que especifica se o símbolo de dados foi dividido em uma agregação ou coleção de outros símbolos; o compilador trata os símbolos como entidades separadas, mesmo que eles realmente façam parte de um símbolo maior.
title: IDiaSymbol::get_isSplitted | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSplitted method
ms.assetid: ff160cf6-003b-4ef5-a406-20a7b287b2bf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5dd9807928ca5f1b8d2e3b20c5de3ec30adc70db
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162050"
---
# <a name="idiasymbolget_issplitted"></a>IDiaSymbol::get_isSplitted
Recupera um sinalizador que especifica se o símbolo de dados foi dividido em uma agregação ou coleção de outros símbolos; o compilador trata os símbolos como entidades separadas, mesmo que eles realmente façam parte de um símbolo maior.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_isSplitted(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>Parâmetros
 `pFlag`

fora Retorna `TRUE` se o símbolo foi dividido em uma agregação de símbolos; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O método [IDiaSymbol:: get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md) retorna `TRUE` para todos os símbolos que fazem parte de um símbolo de divisão.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)
