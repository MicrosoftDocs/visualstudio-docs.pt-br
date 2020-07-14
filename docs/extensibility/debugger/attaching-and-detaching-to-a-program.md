---
title: Anexando e desanexando a um programa | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 42a751e6aa70c1aacd5df598e0c0e62da3b9d14b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903157"
---
# <a name="attaching-and-detaching-to-a-program"></a>Anexando e desanexando a um programa
Anexar o depurador requer o envio da sequência correta de métodos e eventos com os atributos adequados.

## <a name="sequence-of-methods-and-events"></a>Sequência de métodos e eventos

1. O SDM (Gerenciador de depuração de sessão) chama o método [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) .

    Com base no modelo de processo do mecanismo DE depuração (DE), o `IDebugProgramNodeAttach2::OnAttach` método retorna um dos seguintes métodos, que determina o que acontece em seguida.

    Se `S_FALSE` for retornado, o mecanismo de depuração foi anexado com êxito ao programa. Caso contrário, o método [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) será chamado para concluir o processo de anexo.

    Se `S_OK` for retornado, o de será carregado no mesmo processo que o SDM. O SDM executa as seguintes tarefas:

   1. Chama [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) para obter as informações do mecanismo de de.

   2. Cocria o DE.

   3. Chama [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md).

2. O DE envia um [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) para o SDM com um `EVENT_SYNC` atributo.

3. O DE envia um [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) para o SDM com um `EVENT_SYNC` atributo.

4. O DE envia um [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) para o SDM com um `EVENT_SYNC_STOP` atributo.

   A desanexação de um programa é um processo simples de duas etapas, da seguinte maneira:

5. O SDM chama [Detach](../../extensibility/debugger/reference/idebugprogram2-detach.md).

6. O DE envia um [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md).

## <a name="see-also"></a>Confira também
- [Chamando eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
