---
title: Controle de execução | Microsoft Docs
description: Saiba mais sobre como parar eventos, o que significa que o DE espera por uma resposta do usuário por meio do IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 55edea88c5983920b382672d160498b9901ba5ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068018"
---
# <a name="control-of-execution"></a>Controle de execução
O mecanismo de depuração (DE) normalmente envia um dos seguintes eventos como o último evento de inicialização:

- O evento de ponto de entrada, se estiver anexando a um programa recém-lançado

- O evento de carregamento concluído, se estiver anexando a um programa que já está em execução

  Esses dois eventos estão parando eventos, o que significa que o DE espera por uma resposta do usuário por meio do IDE. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md).

## <a name="stopping-event"></a>Interrompendo evento
 Quando um evento de parada é enviado para a sessão de depuração:

1. O programa e o thread que contêm o ponteiro de instrução atual podem ser obtidos na interface de evento.

2. O IDE determina o arquivo de código-fonte atual e a posição, que é exibido como realçado no editor.

3. A sessão de depuração normalmente responde a esse primeiro evento de interrupção chamando o método **continue** do programa.

4. O programa é executado até encontrar uma condição de interrupção, como atingir um ponto de interrupção. Nesse caso, o DE envia um evento de ponto de interrupção para a sessão de depuração. O evento de ponto de interrupção é um evento de interrupção e o DE novamente aguarda uma resposta do usuário.

5. Se o usuário optar por entrar, acima ou fora de uma função, o IDE solicitará que a sessão de depuração chame o método do programa `Step` . Em seguida, o IDE passa a unidade de etapa (instrução, instrução ou linha) e o tipo de etapa (se deseja entrar, acima ou fora da função). Quando a etapa for concluída, o DE enviará um evento DE conclusão de etapa para a sessão de depuração, que é um evento de parada.

    – ou –

    Se o usuário optar por continuar executando a partir do ponteiro de instrução atual, o IDE solicitará a sessão de depuração para chamar o método **Execute** do programa. O programa retoma a execução até encontrar a próxima condição de interrupção.

    – ou –

    Se a sessão de depuração for ignorar um evento de interrupção específico, a sessão de depuração chamará o método **continue** do programa. Se o programa estava passando para cima ou para fora de uma função quando ele encontrou a condição de interrupção, ele continua a etapa.

   Programaticamente, quando o DE encontra uma condição de interrupção, ele envia tais eventos de parada como [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) ou [IDEBUGENTRYPOINTEVENT2](../../extensibility/debugger/reference/idebugentrypointevent2.md) para o SDM (Gerenciador de depuração de sessão) por meio de uma interface [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) . O DE passa as interfaces [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) e [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) que representam o programa e o thread que contém o ponteiro de instrução atual. O SDM chama [IDebugThread2:: EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para obter o quadro de pilha superior e chama [IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) para obter o contexto do documento associado ao ponteiro de instrução atual. Esse contexto de documento normalmente é um nome de arquivo de código-fonte, linha e número de coluna. O IDE usa esses para realçar o código-fonte que contém o ponteiro de instrução atual.

   Normalmente, o SDM responde a esse primeiro evento de interrupção chamando [IDebugProgram2:: Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md). O programa é executado até encontrar uma condição de interrupção, como atingir um ponto de interrupção. nesse caso, o DE envia uma [interface IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) para o SDM. O evento de ponto de interrupção é um evento de interrupção e o DE novamente aguarda uma resposta do usuário.

   Se o usuário optar por entrar, acima ou fora de uma função, o IDE solicitará que o SDM chame [IDebugProgram2:: Step](../../extensibility/debugger/reference/idebugprogram2-step.md). Em seguida, o IDE passa o [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) (instrução, instrução ou linha) e o [STEPKIND](../../extensibility/debugger/reference/stepkind.md), ou seja, se deseja entrar, acima ou fora da função. Quando a etapa é concluída, a DE envia uma interface [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) para o SDM, que é um evento de parada.

   Se o usuário optar por continuar executando a partir do ponteiro de instrução atual, o IDE solicitará que o SDM chame [IDebugProgram2:: execute](../../extensibility/debugger/reference/idebugprogram2-execute.md). O programa retoma a execução até encontrar a próxima condição de interrupção.

   Se o pacote de depuração for ignorar um evento de interrupção específico, o pacote de depuração chamará o SDM, que chama [IDebugProgram2:: Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md). Se o programa estava passando para cima ou para fora de uma função quando ele encontrou a condição de interrupção, ele continua a etapa. Isso implica que o programa mantém um estado de depuração, para que ele saiba como continuar.

   As chamadas que o SDM faz `Step` , **executam** e **continuam** assíncronas, o que significa que o SDM espera que a chamada retorne rapidamente. Se o DE enviar o evento do SDM a parar no mesmo thread antes `Step` , **Execute** ou **continue** retorna, o SDM para de responder.

## <a name="see-also"></a>Confira também
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)
