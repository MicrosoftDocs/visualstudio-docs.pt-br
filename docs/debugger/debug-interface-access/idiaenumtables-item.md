---
title: 'IDiaEnumTables:: item | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Item method
ms.assetid: d65ab262-10c6-48ce-95a3-b5e4cb2c85af
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6a65bdca680bac7c3a5b2e6a5a671045cdef093
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467529"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
Recupera uma tabela por meio de um índice ou nome.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Item ( 
   VARIANT     index,
   IDiaTable** table
);
```

#### <a name="parameters"></a>Parâmetros
 `index`

no Índice ou nome do [IDiaTable](../../debugger/debug-interface-access/idiatable.md) a ser recuperado. Se for usada uma variante de inteiro, ela deverá estar no intervalo de 0 a `count` -1, onde `count` é retornado pelo método [IDiaEnumTables:: get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md) .

 `table`

fora Retorna um objeto [IDiaTable](../../debugger/debug-interface-access/idiatable.md) que representa a tabela desejada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se uma variante de cadeia de caracteres for especificada, a cadeia de caracteres nomeia uma tabela específica. O nome deve ser um dos nomes de tabela, conforme definido em [constantes (debug interface Access SDK)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md).

## <a name="example"></a>Exemplo

```C++
VARIANT var;
var.vt = VT_BSTR;
var.bstrVal = SysAllocString(DiaTable_Symbols );
IDiaTable* pTable;
pEnumTables->Item( var, &pTable );
```

## <a name="see-also"></a>Confira também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)
- [Constantes (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)