---
title: LocationType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2fafbb25d52df6082736431727222c788d73476
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461213"
---
# <a name="locationtype"></a>LocationType
Indica o tipo de informações de local contidas em um símbolo.

## <a name="syntax"></a>Syntax

```C++
enum LocationType {
    LocIsNull,
    LocIsStatic,
    LocIsTLS,
    LocIsRegRel,
    LocIsThisRel,
    LocIsEnregistered,
    LocIsBitField,
    LocIsSlot,
    LocIsIlRel,
    LocInMetaData,
    LocIsConstant,
    LocTypeMax
};
```

## <a name="elements"></a>Elementos
`LocIsNull`As informações de local não estão disponíveis.

`LocIsStatic`O local é estático.

`LocIsTLS`O local está no armazenamento local de thread.

`LocIsRegRel`A localização é relativa ao registro.

`LocIsThisRel`O local é `this` relativo.

`LocIsEnregistered`O local está em um registro.

`LocIsBitField`O local está em um campo de bits.

`LocIsSlot`O local é um slot MSIL (Microsoft Intermediate Language).

`LocIsIlRel`O local é MSIL-Relative.

`LocInMetaData`O local está nos metadados.

`LocIsConstant`O local está em um valor constante.

`LocTypeMax`O número de tipos de local nesta enumeração.

## <a name="remarks"></a>Comentários
As propriedades disponíveis para a interface [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) dependem do local do símbolo dentro do arquivo de imagem. Para obter mais informações, consulte [locais de símbolo](../../debugger/debug-interface-access/symbol-locations.md).

Os valores nessa enumeração são retornados por uma chamada para o método [IDiaSymbol:: get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [Locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md)
