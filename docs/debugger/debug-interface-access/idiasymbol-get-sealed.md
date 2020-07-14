---
title: IDiaSymbol::get_sealed | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_sealed method
ms.assetid: cd1fef1f-47de-47c7-885f-f6f0a9a07d8c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0b1f826c4dfcc8f000b37144b28dfcb8cf503a87
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462049"
---
# <a name="idiasymbolget_sealed"></a>IDiaSymbol::get_sealed
Recupera um sinalizador que especifica se a classe ou o método está lacrado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_sealed( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se a classe ou o método é lacrado; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Uma classe sealed não pode ser usada como uma classe base. Um método lacrado não pode ser Overidden.

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia100.dll

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)