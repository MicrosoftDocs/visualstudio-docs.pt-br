---
title: IDiaSymbol::get_hasEH | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasEH method
ms.assetid: 9a4952d8-9fa7-4798-b48c-fe4357648276
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d387d37103773e7352357ebef5f9134bcff85c59
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99854244"
---
# <a name="idiasymbolget_haseh"></a>IDiaSymbol::get_hasEH
Recupera um sinalizador que especifica se a função contém qualquer manipulação de exceção de estilo C++ não gerenciado (por exemplo, um bloco try/catch).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_hasEH(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>Parâmetros
 `pFlag`

fora Retorna `TRUE` se a função tem qualquer manipulação de exceção em estilo C++; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Consulte também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)