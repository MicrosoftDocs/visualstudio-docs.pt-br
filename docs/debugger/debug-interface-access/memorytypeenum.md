---
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 2cd255ab59c9d46676ba46baddd9cee7e3ef4cc2
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461178"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
Especifica o tipo de memória a ser acessado.

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
`MemTypeCode`Acessa apenas a memória de código.

`MemTypeData`Acessa dados ou pilha de memória.

`MemTypeStack`Acessa apenas a memória de pilha.

`MemTypeAny`Acessa qualquer tipo de memória.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são passados para o método [IDiaStackWalkHelper:: readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md) para limitar o acesso a diferentes tipos de memória.

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
