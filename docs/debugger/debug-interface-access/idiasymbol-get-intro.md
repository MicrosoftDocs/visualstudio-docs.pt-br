---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b48f91dcb68f44f070e596d674461367dcf22966
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463515"
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

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
