---
description: Descreve uma entrada em um mapa de endereços.
title: DiaAddressMapEntry | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bdac0233901ac8571bbfb2a5d6659adf69e35298
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149189"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
Descreve uma entrada em um mapa de endereços.

## <a name="syntax"></a>Sintaxe

```C++
struct DiaAddressMapEntry {
    DWORD rva,
    DWORD rvaTo
};
```

## <a name="elements"></a>Elementos
`rva` Um RVA (endereço virtual relativo) na imagem A.

`rvaTo` O endereço virtual relativo `rva` é mapeado para a imagem B.

## <a name="remarks"></a>Comentários
Um mapa de endereços fornece uma tradução de um layout de imagem (A) para outro (B). Uma matriz de `DiaAddressMapEntry` estruturas classificada por `rva` define um mapa de endereços.

Para converter um endereço, `addrA` , na imagem a para um endereço, `addrB` , na imagem B, execute as seguintes etapas:

1. Pesquise o mapa para a entrada, `e` , com o maior `rva` menor ou igual a `addrA` .

2. Defina `delta = addrA - e.rva`.

3. Defina `addrB = e.rvaTo + delta`.

    Uma matriz de `DiaAddressMapEntry` estruturas é passada para o método [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

## <a name="see-also"></a>Confira também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
