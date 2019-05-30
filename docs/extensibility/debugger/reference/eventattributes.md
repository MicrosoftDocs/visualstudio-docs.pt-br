---
title: EVENTATTRIBUTES | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a3361d27a9e0a4a1f56035c0d2af20d9fa9a9303
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337763"
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
Indica que o evento é assíncrono e não é necessária nenhuma resposta ao evento.

`EVENT_SYNCHRONOUS`\
Indica que o evento é síncrono; responder por meio da [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md).

`EVENT_STOPPING`\
Indica que se trata de um evento de interrupção. Deve ser combinado com o `EVENT_ASYNCHRONOUS` ou `EVENT_SYNCHRONOUS`.

`EVENT_ASYNC_STOP`\
Indica um evento de interrupção assíncrono. Atualmente, não há nenhum evento do tipo. Este sinalizador é apenas um espaço reservado.

`EVENT_SYNC_STOP`\
Indica um evento de interrupção síncrona (uma combinação de `EVENT_SYNCHRONOUS` e `EVENT_STOPPING`). Esse valor é usado por um mecanismo de depuração (DES) quando ele envia um evento de interrupção. A resposta é feita por meio de uma chamada para [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md), [etapa](../../../extensibility/debugger/reference/idebugprogram2-step.md), ou [continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md).

`EVENT_IMMEDIATE`\
Indica um evento que é enviado imediatamente e de forma síncrona para o IDE. Esse sinalizador é combinado com outros sinalizadores como `EVENT_ASYNCHRONOUS`, `EVENT_SYNCHRONOUS`, ou `EVENT_SYNC_STOP` para indicar o tipo de evento e o fato de que o mecanismo de resposta (se houver) é conhecido.

`EVENT_EXPRESSION_EVALUATION`\
O evento é um resultado da avaliação de expressão.

## <a name="remarks"></a>Comentários
Esses valores são passados no `dwAttrib` parâmetro do [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) método.

Esses valores podem ser combinados com um bit a bit `OR`.

## <a name="requirements"></a>Requisitos
Header: msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
