---
title: IDiaSymbol::get_lexicalParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_lexicalParent method
ms.assetid: 4d119965-33a8-474c-9c64-95c5218c389c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1a381fe495208bf3dd1f530a2d5e3dffd7c3c76
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463060"
---
# <a name="idiasymbolget_lexicalparent"></a>IDiaSymbol::get_lexicalParent
Recupera uma referência ao pai léxico do símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_lexicalParent ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o pai léxico do símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O pai léxico de um símbolo é a função ou o módulo delimitador. Por exemplo, o pai léxico de um parâmetro de função ou variável local é a própria função enquanto o pai léxico da função é o módulo em que ele está definido.

 Os possíveis símbolos que podem aparecer como pais léxicos são documentados na [hierarquia lexical dos tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md).

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)