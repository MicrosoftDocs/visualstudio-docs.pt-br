---
title: IDiaSymbol::get_unmodifiedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_unmodifiedType method
ms.assetid: bf914dc0-ff84-4f5d-9f75-1733b17f3be0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee138fd361d883fb465711e679d09e6c96ddac4b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461577"
---
# <a name="idiasymbolget_unmodifiedtype"></a>IDiaSymbol::get_unmodifiedType
Recupera o tipo original deste símbolo. Use quando a [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) for definida como um tipo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_unmodifiedType( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o tipo original deste símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O tipo atual é uma modificação do tipo original retornado. O tipo original de um símbolo pode ser determinado pela primeira vez que obter o tipo do símbolo e, em seguida, interrogar esse tipo retornado para o tipo original. Observe que alguns símbolos podem não ter um tipo modificado do tipo original.

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia100.dll

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)