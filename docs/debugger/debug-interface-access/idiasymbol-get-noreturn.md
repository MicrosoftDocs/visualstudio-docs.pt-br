---
title: IDiaSymbol::get_noReturn | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noReturn method
ms.assetid: 704c1cc0-5b84-4334-a02a-70f43aff39d5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0857939289091d22aaafb5dc5bb009d4af0e00bb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63399329"
---
# <a name="idiasymbolgetnoreturn"></a>IDiaSymbol::get_noReturn
Recupera um sinalizador que especifica se a função foi marcada como de retorno nunca com o [noreturn](/cpp/cpp/noreturn) atributo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_noReturn(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>Parâmetros
 pFlag

[out] Retorna `TRUE` se a função foi declarada como de retorno nunca com o `noreturn` atributo; caso contrário, retornará `FALSE`.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|V DIA SDK 8.0|

## <a name="see-also"></a>Consulte também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [noreturn](/cpp/cpp/noreturn)