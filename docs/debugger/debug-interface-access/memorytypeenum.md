---
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6e0f0973c0491cd65c2d03be785bb03b8c2f31df
ms.sourcegitcommit: 22b73c601f88c5c236fe81be7ba4f7f562406d75
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56227414"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
Especifica o tipo de memória para acessar.

## <a name="syntax"></a>Sintaxe

```C++
enum MemoryTypeEnum {
    MemTypeCode,
    MemTypeData,
    MemTypeStack,
    MemTypeAny = -1
};
```

#### <a name="parameters"></a>Parâmetros
`MemTypeCode`  
Acessos de memória somente código.

`MemTypeData`  
Memória de dados ou a pilha de acessos.

`MemTypeStack`  
Acessos apenas memória de pilha.

`MemTypeAny`  
Acessa qualquer tipo de memória.

## <a name="remarks"></a>Comentários
Os valores nesta enumeração são passados para o [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md) método para limitar o acesso a diferentes tipos de memória.

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst.h

## <a name="see-also"></a>Consulte também
[Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)  
[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
