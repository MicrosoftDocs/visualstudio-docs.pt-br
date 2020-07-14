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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f83cdb163881366a1a0bede95a07e1dae1fc50a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461094"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
Especifica o tipo de quadro de pilha.

## <a name="syntax"></a>Syntax

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
`FrameTypeFPO`Ponteiro de quadro omitido; Informações de FPO disponíveis.

`FrameTypeTrap`Quadro de interceptação do kernel.

`FrameTypeTSS`Quadro de interceptação do kernel.

`FrameTypeStandard`Quadro de pilha EBP padrão.

`FrameTypeFrameData`Ponteiro de quadro omitido; Informações de dados de quadro disponíveis.

`FrameTypeUnknown`Quadro que não tem nenhuma informação de depuração.

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados por uma chamada para o método [IDiaStackFrame:: get_Type](../../debugger/debug-interface-access/idiastackframe-get-type.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
