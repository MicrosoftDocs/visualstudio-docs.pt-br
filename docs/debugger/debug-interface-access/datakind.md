---
title: DataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2423646976744da17d3e904246ac74f8b2e75f41
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468703"
---
# <a name="datakind"></a>DataKind
Indica o escopo específico de um valor de dados.

## <a name="syntax"></a>Syntax

```C++
enum DataKind {
    DataIsUnknown,
    DataIsLocal,
    DataIsStaticLocal,
    DataIsParam,
    DataIsObjectPtr,
    DataIsFileStatic,
    DataIsGlobal,
    DataIsMember,
    DataIsStaticMember,
    DataIsConstant
};
```

## <a name="elements"></a>Elementos
O símbolo de dados DataIsUnknown não pode ser determinado.

O item de dados DataIsLocal é uma variável local.

O item de dados DataIsStaticLocal é uma variável local estática.

O item de dados DataIsParam é um parâmetro formal.

O item de dados DataIsObjectPtr é um ponteiro de objeto ( `this` ).

O item de dados DataIsFileStatic é uma variável com escopo de arquivo.

O item de dados DataIsGlobal é uma variável global.

O item de dados DataIsMember é uma variável de membro de objeto.

O item de dados DataIsStaticMember é uma variável estática de classe.

O item de dados DataIsConstant é um valor constante.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados pelo método [IDiaSymbol:: get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)
