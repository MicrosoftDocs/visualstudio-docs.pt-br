---
title: IDiaSymbol::get_baseType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_baseType method
ms.assetid: 5c69a241-a8d3-48ed-8b36-27463a196572
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aea1205abf5c7a4bf7e4fd6b035651cc7ad52be6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464201"
---
# <a name="idiasymbolget_basetype"></a>IDiaSymbol::get_baseType
Recupera o tipo base deste símbolo<em>.</em>

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_baseType (
    DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
`pRetVal`

fora Retorna um valor da enumeração de [Enumeração BasicType](../../debugger/debug-interface-access/basictype.md) especificando o tipo base do símbolo.

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
O tipo básico para um símbolo pode ser determinado pela primeira vez que obter o tipo do símbolo e, em seguida, interrogar esse tipo retornado para o tipo base. Observe que alguns símbolos podem não ter um tipo base — por exemplo, um nome de estrutura.

## <a name="example"></a>Exemplo

```C++
IDiaSymbol* pType;
CComPtr<IDiaSymbol> pBaseType;
if (pType->get_type( &pBaseType ) == S_OK)
{
    BasicType btBaseType;
    if (pBaseType->get_baseType((DWORD *)&btBaseType) == S_OK)
    {
        // Do something with basic type.
    }
}
```

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração BasicType](../../debugger/debug-interface-access/basictype.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
