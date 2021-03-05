---
description: Recupera um sinalizador que especifica se a função é uma função virtual de introdução.
title: IDiaSymbol::get_intro | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intro method
ms.assetid: 101afe4a-4c57-45de-87b4-330394c6de10
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ad2e791995f4edc1b09655640bc339d577f7f37d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160872"
---
# <a name="idiasymbolget_intro"></a>IDiaSymbol::get_intro
Recupera um sinalizador que especifica se a função é uma função virtual de introdução.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_intro ( 
    BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
`pRetVal`

fora Retorna `TRUE` se a função é de introdução virtual; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="example"></a>Exemplo

```C++
class A {
    virtual int f1();
}
class B : public A {
    int f1();
}
```

Ambos `A::f1` e `B::f1` são funções virtuais, mas `A::f1` é a introdução virtual.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
