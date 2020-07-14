---
title: IDiaSymbol::get_hasSEH | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSEH method
ms.assetid: 1a709ded-22c8-464c-97be-eba5e464210c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e0f9e7b1dc2fb5a338dc2cd2edbf3cf9d0eb2441
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463662"
---
# <a name="idiasymbolget_hasseh"></a>IDiaSymbol::get_hasSEH
Recupera um sinalizador que especifica se a função contém qualquer [manipulação de exceção estruturada (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp) (por exemplo, blocos de __try/ \_ _except).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_hasSEH(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>Parâmetros
 `pFlag`

fora Retorna `TRUE` se a função tem qualquer bloco de manipulação de exceção estruturado; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Manipulação de exceção estruturada (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp)