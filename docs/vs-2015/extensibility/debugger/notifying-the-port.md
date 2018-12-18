---
title: Notificar a porta | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c3cfcc4ee357301aa0e38468b13b983c3d5ca55a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763368"
---
# <a name="notifying-the-port"></a>Notificando a porta
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

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
 [Iniciar um programa](../../extensibility/debugger/launching-a-program.md)   
 [Anexar após uma inicialização](../../extensibility/debugger/attaching-after-a-launch.md)   
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)

