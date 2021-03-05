---
description: Recupera o designador de registro do local quando a enumeração LocationType é definida como LocIsEnregistered '.
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3f6845c83b46fb524221933eb859742ebe7a95e6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161896"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
Recupera o designador de registro do local quando a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) é definida como `LocIsEnregistered` .

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o designador de registro do local.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Se o símbolo for relativo a um registro, ou seja, se a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) do símbolo for definida como `LocIsRegRel` , use o `get_registerId` método seguido por uma chamada para o método [IDiaSymbol:: get_Offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) para obter o deslocamento do registro onde o símbolo está localizado.

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md)
