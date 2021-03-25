---
description: Especifica os atributos do evento.
title: EVENTOATTRIBUTES | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 922c60c0bb36c58b88c2422580eeda0db1c02d42
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059477"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
Especifica os atributos do evento.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
typedef DWORD EVENTATTRIBUTES;
```

```csharp
public enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
```

## <a name="fields"></a>Campos
`EVENT_ASYNCHRONOUS`\
Indica que o evento é assíncrono e nenhuma resposta ao evento é necessária.

`EVENT_SYNCHRONOUS`\
Indica que o evento é síncrono; responder por meio de [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md).

`EVENT_STOPPING`\
Indica que se trata de um evento de parada. Deve ser combinado com um `EVENT_ASYNCHRONOUS` ou `EVENT_SYNCHRONOUS` .

`EVENT_ASYNC_STOP`\
Indica um evento de parada assíncrona. Atualmente, não há tal evento. Esse sinalizador é apenas um espaço reservado.

`EVENT_SYNC_STOP`\
Indica um evento de interrupção síncrono (uma combinação de `EVENT_SYNCHRONOUS` e `EVENT_STOPPING` ). Esse valor é usado por um mecanismo DE depuração (DE) ao enviar um evento de parada. A resposta é feita por meio de uma chamada para [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md), [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)ou [continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md).

`EVENT_IMMEDIATE`\
Indica um evento que é enviado imediatamente e de forma síncrona ao IDE. Esse sinalizador é combinado com outros sinalizadores como `EVENT_ASYNCHRONOUS` , `EVENT_SYNCHRONOUS` ou `EVENT_SYNC_STOP` para indicar o tipo de evento e o fato de que o mecanismo de resposta (se houver) é conhecido.

`EVENT_EXPRESSION_EVALUATION`\
O evento é um resultado da avaliação da expressão.

## <a name="remarks"></a>Comentários
Esses valores são passados no `dwAttrib` parâmetro do método de [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) .

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
