---
title: Iniciando o depurador | Microsoft Docs
description: Saiba mais sobre a sequência de métodos e eventos com seus atributos adequados necessários para iniciar o depurador.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67764a7f59c1b44e7e8cbc7a81befb120c541461
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094660"
---
# <a name="launch-the-debugger"></a>Iniciar o depurador
Iniciar o depurador requer o envio da sequência correta de métodos e eventos com seus atributos adequados.

## <a name="sequences-of-methods-and-events"></a>Sequências de métodos e eventos

1. O SDM (Gerenciador de depuração de sessão) é chamado escolhendo o menu **depurar** e, em seguida, escolhendo **Iniciar**. Para obter mais informações, consulte [Iniciar um programa](../../extensibility/debugger/launching-a-program.md).

2. O SDM chama o método [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) .

3. Com base no modelo de processo do mecanismo DE depuração (DE), o `IDebugProgramNodeAttach2::OnAttach` método retorna um dos seguintes métodos, que determina o que acontece em seguida.

     Se `S_FALSE` retornar, o mecanismo de depuração (de) deve ser carregado no processo da máquina virtual.

     – ou –

     Se `S_OK` retornar, o de será carregado no processo do SDM. O SDM executa as seguintes tarefas:

    1. Chama [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) para obter as informações do mecanismo de de.

    2. Cocria o DE.

    3. Chama [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md).

4. O DE envia um [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) para o SDM com um `EVENT_SYNC` atributo.

5. O DE envia um [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) para o SDM com um `EVENT_SYNC` atributo.

6. O DE envia um [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) para o SDM com um `EVENT_SYNC` atributo.

7. O DE envia um [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) para o SDM com um `EVENT_SYNC` atributo.

8. O DE envia um [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) para o SDM com um `EVENT_SYNC` atributo.

## <a name="see-also"></a>Confira também
- [Chamando eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
- [Iniciando um programa](../../extensibility/debugger/launching-a-program.md)
