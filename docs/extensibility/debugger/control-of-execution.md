---
title: Controle de execução | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 42a95e01a44236d4f98f55f50a56cf28473ad575
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927535"
---
# <a name="control-of-execution"></a>Controle de execução
O mecanismo de depuração (DES) normalmente envia um dos seguintes eventos como o último evento de inicialização:  
  
- O evento de ponto de entrada, se anexar a um programa recém-iniciado  
  
- O evento de carga concluída, se anexar a um programa que já está em execução  
  
  Ambos esses eventos são eventos de parada, que significa que o DE aguarda uma resposta do usuário por meio do IDE. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md).  
  
## <a name="stopping-event"></a>Interrompendo o evento  
 Quando um evento de interrupção é enviado para a sessão de depuração:  
  
1. O programa e o thread que contêm o ponteiro de instrução atual podem ser obtidos a partir da interface do evento.  
  
2. O IDE determina que o arquivo de código-fonte atual e a posição, que são exibidos como destacado no editor.  
  
3. A sessão de depuração normalmente responde a este evento de interrupção primeiro chamando o programa **continuar** método.  
  
4. O programa é executado, em seguida, até encontrar uma condição de interrupção, como atingir um ponto de interrupção. Nesse caso, o DE envia um evento de ponto de interrupção para a sessão de depuração. O ponto de interrupção é um evento de interrupção e o DE novamente aguarda uma resposta do usuário.  
  
5. Se o usuário opta por intervir, encerrar ou sair de uma função, o IDE solicita que a sessão de depuração para chamar o programa `Step` método. O IDE, em seguida, passa a unidade da etapa (instrução, a instrução ou linha) e o tipo de etapa (seja para a etapa em, acima ou da função). Quando a etapa for concluída, o DE envia um evento de conclusão da etapa para a sessão de depuração, que é um evento de interrupção.  
  
    -ou-  
  
    Se o usuário opta por continuar a execução do ponteiro de instrução atual, o IDE solicita que a sessão de depuração para chamar o programa **Execute** método. O programa retoma a execução até que ele encontra a próxima condição de interrupção.  
  
    -ou-  
  
    Se a sessão de depuração é ignorar um evento de interrupção específico, a sessão de depuração chama o programa **continuar** método. Se o programa foi passo a passo em, acima ou fora de uma função quando ela encontrada a condição de interrupção, ele continua a etapa.  
  
   Programaticamente, quando o DE encontra uma condição de interrupção, ele envia eventos como parando [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) ou [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) para o Gerenciador de depuração de sessão (SDM) por meio de uma [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) interface. Os passos do [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) e [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) interfaces que representam o programa e o thread que contém o ponteiro de instrução atual. As chamadas SDM [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para obter o quadro superior da pilha e chama [IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) para obter o contexto de documento associado com a instrução atual ponteiro. Este contexto de documento normalmente é um número de coluna, linha e nome de arquivo do código fonte. O IDE usa estes para realçar o código-fonte que contém o ponteiro de instrução atual.  
  
   O SDM normalmente responde a este evento de interrupção primeiro chamando [IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md). O programa é executado, em seguida, até encontrar uma condição de interrupção, como atingir um ponto de interrupção, em que envia o caso DE um [IDebugBreakpointEvent2 Interface](../../extensibility/debugger/reference/idebugbreakpointevent2.md) para o SDM. O ponto de interrupção é um evento de interrupção e o DE novamente aguarda uma resposta do usuário.  
  
   Se o usuário opta por intervir, encerrar ou sair de uma função, o IDE avisará o SDM para chamar [IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md). O IDE, em seguida, passa o [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) (instrução, a instrução ou linha) e o [STEPKIND](../../extensibility/debugger/reference/stepkind.md), ou seja, se a etapa em, acima ou da função. Quando a etapa for concluída, o DE envia um [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) interface para o SDM, o que é um evento de interrupção.  
  
   Se o usuário opta por continuar a execução do ponteiro de instrução atual, o IDE solicita o SDM para chamar [IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md). O programa retoma a execução até que ele encontra a próxima condição de interrupção.  
  
   Se o pacote de depuração é ignorar um evento de interrupção específico, o pacote de depuração chama o SDM, que chama [IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md). Se o programa foi passo a passo em, acima ou fora de uma função quando ela encontrada a condição de interrupção, ele continua a etapa. Isso implica que o programa mantém um estado de passo a passo, para que ele saiba como continuar.  
  
   As chamadas que faz o SDM `Step`, **Execute**, e **continuar** são assíncrona, o que significa que o SDM espera que a chamada para retornar rapidamente. Se o DE envia o SDM um evento de interrupção no mesmo thread antes `Step`, **Execute**, ou **continuar** retorna, o SDM para de responder.  
  
## <a name="see-also"></a>Consulte também  
 [As tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)