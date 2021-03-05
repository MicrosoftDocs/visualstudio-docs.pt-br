---
description: Recupera um sinalizador que especifica se a função contém qualquer manipulação de exceção estruturada (C/C++)) (por exemplo, blocos de _try/__except).
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a802a14c1c4e9b9c3b080c751d8cd512c3adf75d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102156262"
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

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Tratamento de exceções estruturado (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp)
