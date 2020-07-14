---
title: IDiaSymbol::get_type | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_type method
ms.assetid: 1c6a4176-dd4e-4c22-8b8f-0e559fc078ba
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 738d3045c524700e803fe82c8902d4f1b77948b5
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461742"
---
# <a name="idiasymbolget_type"></a>IDiaSymbol::get_type
Recupera o símbolo que representa o tipo deste símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_type (
    IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
`pRetVal`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o tipo deste símbolo.

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
Para determinar o tipo de símbolo, você deve chamar esse método e examinar o objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) resultante. Observe que é possível que um símbolo não tenha um tipo. Por exemplo, o nome de uma estrutura não tem nenhum tipo, mas pode ter símbolos filhos (use o método [IDiaSymbol:: findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md) para examinar esses filhos).

## <a name="example"></a>Exemplo

```C++
IDiaSymbol*         pType;
CComPtr<IDiaSymbol> pBaseType;
if (SUCCEEDED(pType->get_type( &pBaseType ))) {
    BasicType btBaseType;
    if (SUCCEEDED(pBaseType->get_baseType((DWORD *)&btBaseType))) {
        // Do something with basic type.
    }
}
```

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
