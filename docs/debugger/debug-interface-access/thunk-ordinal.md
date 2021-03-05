---
description: Designa tipos de conversão.
title: THUNK_ORDINAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8d9fe78eedd0166594daf43093aa525e3d8d3e88
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161588"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
Designa tipos de conversão.

## <a name="syntax"></a>Sintaxe

```C++
typedef enum THUNK_ORDINAL {
    THUNK_ORDINAL_NOTYPE,
    THUNK_ORDINAL_ADJUSTOR,
    THUNK_ORDINAL_VCALL,
    THUNK_ORDINAL_PCODE,
    THUNK_ORDINAL_LOAD

    // trampoline thunk ordinals - only for use in Trampoline thunk symbols
    THUNK_ORDINAL_TRAMP_INCREMENTAL,
    THUNK_ORDINAL_TRAMP_BRANCHISLAND,
} THUNK_ORDINAL;
```

## <a name="elements"></a>Elementos
THUNK_ORDINAL_NOTYPE conversão padrão.

THUNK_ORDINAL_ADJUSTOR uma `this` conversão de ajustador.

Conversão de chamada virtual THUNK_ORDINAL_VCALL.

Conversão de código P THUNK_ORDINAL_PCODE.

Conversão de carga de THUNK_ORDINAL_LOAD atraso.

THUNK_ORDINAL_TRAMP_INCREMENTAL conversão incremental de trampoline (uma conversão de trampoline é usada para chamar chamadas de um espaço de memória para outro).

THUNK_ORDINAL_TRAMP_BRANCHISLAND conversão de ponto de ramificação trampoline.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados de uma chamada para o método [IDiaSymbol:: get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Confira também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)
