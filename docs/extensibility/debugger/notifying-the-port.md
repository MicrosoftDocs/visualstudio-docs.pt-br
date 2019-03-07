---
title: Notificar a porta | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b022cca2b69c8cb80b24fa34e3b020923cff4022
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56689194"
---
# <a name="notify-the-port"></a>Notificar a porta
Depois de iniciar um programa, a porta deve ser notificada, da seguinte maneira:

1. Quando uma porta recebe um novo nó de programa, ele envia um evento de criação do programa volta para a sessão de depuração. O evento carrega uma interface que representa o programa.

2. A sessão de depuração consulta o programa para o identificador de um mecanismo de depuração (DES) que pode se conectar ao.

3. A sessão de depuração verifica se o DE está na lista de permitidos DEs para que o programa. A sessão de depuração obtém essa lista de configurações de programa ativo da solução, originalmente passadas para ele, o pacote de depuração.

    O DE deve estar na lista de permitidos, senão a DE não será anexada ao programa.

   Programaticamente, quando uma porta primeiro recebe um novo nó de programa, ele cria um [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) interface para representar o programa.

> [!NOTE]
>  Isso não deve ser confundido com o `IDebugProgram2` interface criada posteriormente pelo mecanismo de depuração (DES).

 A porta envia um [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) evento de criação do programa volta para o Gerenciador de depuração de sessão (SDM) por meio de uma COM `IConnectionPoint` interface.

> [!NOTE]
>  Isso não deve ser confundido com o `IDebugProgramCreateEvent2` interface, que é enviada mais tarde por DE.

 Junto com a interface de eventos em si, a porta envia o [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md), [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md), e [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) interfaces, que representam a porta, processam, e programa, respectivamente. As chamadas SDM [IDebugProgram2::GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) para obter o GUID do DE que poderá depurar o programa. O GUID foi originalmente obtido o [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) interface.

 O SDM verifica se o DE está na lista de permitidos DEs. O SDM obtém essa lista de configurações de programa ativo da solução, originalmente passadas para ele, o pacote de depuração. O DE deve estar na lista de permitidos, caso contrário, ele não será anexado ao programa.

 Depois que a identidade do DE é conhecida, o SDM está pronto para anexá-lo para o programa.

## <a name="see-also"></a>Consulte também
- [Iniciar um programa](../../extensibility/debugger/launching-a-program.md)
- [Anexar após uma inicialização](../../extensibility/debugger/attaching-after-a-launch.md)
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)