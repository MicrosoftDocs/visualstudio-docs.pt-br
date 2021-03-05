---
description: Recupera o tipo de conversão de uma função.
title: IDiaSymbol::get_thunkOrdinal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thunkOrdinal method
ms.assetid: 4b28d78a-1974-4d8a-8bb7-781bf630f2f4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: de9b0fa692ff44096e962bc952b91c3f2fd314f2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160606"
---
# <a name="idiasymbolget_thunkordinal"></a>IDiaSymbol::get_thunkOrdinal
Recupera o tipo de conversão de uma função.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_thunkOrdinal ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um valor da enumeração de [enumeração THUNK_ORDINAL](../../debugger/debug-interface-access/thunk-ordinal.md) que especifica o tipo de conversão de uma função.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Essa propriedade será válida somente se o símbolo como um valor de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) de `SymTagThunk` .

 Uma "conversão" é um trecho de código que converte entre um espaço de endereço de memória de 32 bits (também conhecido como espaço de endereço simples) e um espaço de endereço de 16 bits (conhecido como um espaço de endereço segmentado).

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração THUNK_ORDINAL](../../debugger/debug-interface-access/thunk-ordinal.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
