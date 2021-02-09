---
title: StackFrameTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 707b22693afe83f82a30055f0c59ff89272b5bc3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99862286"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
Especifica o tipo de quadro de pilha.

## <a name="syntax"></a>Sintaxe

```C++
enum StackFrameTypeEnum {
    FrameTypeFPO,
    FrameTypeTrap,
    FrameTypeTSS,
    FrameTypeStandard,
    FrameTypeFrameData,
    FrameTypeUnknown = -1
};
```

## <a name="elements"></a>Elementos
`FrameTypeFPO` Ponteiro de quadro omitido; Informações de FPO disponíveis.

`FrameTypeTrap` Quadro de interceptação do kernel.

`FrameTypeTSS` Quadro de interceptação do kernel.

`FrameTypeStandard` Quadro de pilha EBP padrão.

`FrameTypeFrameData` Ponteiro de quadro omitido; Informações de dados de quadro disponíveis.

`FrameTypeUnknown` Quadro que não tem nenhuma informação de depuração.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados por uma chamada para o método [IDiaStackFrame:: get_Type](../../debugger/debug-interface-access/idiastackframe-get-type.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Consulte também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
