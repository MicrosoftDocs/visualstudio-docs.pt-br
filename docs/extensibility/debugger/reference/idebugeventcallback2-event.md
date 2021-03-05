---
description: Envia a notificação de eventos de depuração.
title: 'IDebugEventCallback2:: Event | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2::Event
helpviewer_keywords:
- IDebugEventCallback2::Event
ms.assetid: e5a3345b-d460-4e40-8f5b-3111c56a2ed9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afa0cfd8f96d21a510370a4fc526a3cae053c77b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152917"
---
# <a name="idebugeventcallback2event"></a>IDebugEventCallback2::Event
Envia a notificação de eventos de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Event( 
   IDebugEngine2*  pEngine,
   IDebugProcess2* pProcess,
   IDebugProgram2* pProgram,
   IDebugThread2*  pThread,
   IDebugEvent2*   pEvent,
   REFIID          riidEvent,
   DWORD           dwAttrib
);
```

```csharp
int Event( 
   IDebugEngine2  pEngine,
   IDebugProcess2 pProcess,
   IDebugProgram2 pProgram,
   IDebugThread2  pThread,
   IDebugEvent2   pEvent,
   ref Guid       riidEvent,
   uint           dwAttrib
);
```

## <a name="parameters"></a>Parâmetros
`pEngine`\
no Um objeto [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) que representa o mecanismo de depuração (de) que está enviando este evento. Um DE é necessário para preencher esse parâmetro.

`pProcess`\
no Um objeto [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) que representa o processo no qual o evento ocorre. Esse parâmetro é preenchido pelo SDM (Gerenciador de depuração de sessão). Um DE sempre passa um valor nulo para esse parâmetro.

`pProgram`\
no Um objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa no qual esse evento ocorre. Para a maioria dos eventos, esse parâmetro não é um valor nulo.

`pThread`\
no Um objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o thread no qual esse evento ocorre. Para parar eventos, esse parâmetro não pode ser um valor nulo, pois o quadro de pilha é obtido desse parâmetro.

`pEvent`\
no Um objeto [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) que representa o evento de depuração.

`riidEvent`\
no GUID que identifica qual interface de evento obter do `pEvent` parâmetro.

`dwAttrib`\
no Uma combinação de sinalizadores da enumeração do [eventoattributes](../../../extensibility/debugger/reference/eventattributes.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Ao chamar esse método, o `dwAttrib` parâmetro deve corresponder ao valor retornado do método [GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md) conforme chamado no objeto de evento passado no `pEvent` parâmetro.

 Todos os eventos de depuração são postados de forma assíncrona, independentemente se um evento é assíncrono ou não. Quando um DE chama esse método, o valor de retorno não indica se o evento foi processado, somente se o evento foi recebido. Na verdade, na maioria das circunstâncias, o evento não foi processado quando esse método retorna.

## <a name="see-also"></a>Confira também
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
