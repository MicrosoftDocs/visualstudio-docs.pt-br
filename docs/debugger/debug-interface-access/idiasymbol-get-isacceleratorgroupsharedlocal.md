---
description: Recupera um sinalizador que indica se o símbolo corresponde a uma variável local compartilhada de grupo no código compilado para um acelerador de C++ AMP.
title: IDiaSymbol::get_isAcceleratorGroupSharedLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8da1e0e8672fb0c10769ca448556f0007fe44014
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147299"
---
# <a name="idiasymbolget_isacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
Recupera um sinalizador que indica se o símbolo corresponde a uma variável local compartilhada de grupo no código compilado para um acelerador de C++ AMP.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_isAcceleratorGroupSharedLocal(
   BOOL* pFlag);
```

#### <a name="parameters"></a>Parâmetros
 `pFlag`

fora Um ponteiro para um `BOOL` que indica se o símbolo corresponde a uma variável local compartilhada de grupo no código compilado para um acelerador de C++ amp. Se `TRUE` , os `get_baseDataSlot` `get_baseDataOffset` métodos e podem ser usados para obter as informações de local de armazenamento da variável.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)
- [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)
