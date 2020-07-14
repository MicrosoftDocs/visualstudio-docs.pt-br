---
title: 'IDiaSymbol:: get_framePointerPresent | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePointerPresent method
ms.assetid: d036090a-1651-454d-9130-b798f58ba053
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5ccc4c679c7bb20d5b419fe2c04ab5ea8dce904
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463900"
---
# <a name="idiasymbolget_framepointerpresent"></a>IDiaSymbol::get_framePointerPresent
Recupera um sinalizador que especifica se o ponteiro do quadro está presente. Use quando a [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) for definida como `SymTagFunction` .

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_framePointerPresent( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

[fora]] Retorna `TRUE` se o ponteiro do quadro estiver presente; caso contrário, retornará `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia100.dll

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)