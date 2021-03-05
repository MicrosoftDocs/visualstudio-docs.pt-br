---
description: Recupera o número de bits ou bytes de memória usados pelo objeto representado por esse símbolo.
title: IDiaSymbol::get_length | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_length method
ms.assetid: cc62f028-d195-4fbf-93bc-10b08bef52d2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a7b3a7a88c688f8ff68f2c1280390f10110c3a9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162008"
---
# <a name="idiasymbolget_length"></a>IDiaSymbol::get_length
Recupera o número de bits ou bytes de memória usados pelo objeto representado por esse símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_length ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de bytes ou bits de memória usados pelo objeto representado por este símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Se a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) do símbolo for `LocIsBitField` , o comprimento retornado por esse método será em bits; caso contrário, o comprimento será em bytes para todos os outros tipos de local.

## <a name="example"></a>Exemplo

```C++
IDiaSymbol* pSymbol;
ULONGLONG   length;
pSymbol->get_length( &length );
```

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md)
