---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c2bae3d054aa8e331db3a345743e4f0e9c20b49
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463172"
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

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)