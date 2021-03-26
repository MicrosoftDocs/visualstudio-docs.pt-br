---
title: Anexando após uma inicialização | Microsoft Docs
description: Quando um programa é iniciado, a sessão de depuração está pronta para anexar o mecanismo de depuração ao programa. Escolha uma abordagem de design para comunicação com o mecanismo de depuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9010d2619b76c2932ca1a8a5aed8db6c6a5cf075
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055317"
---
# <a name="attach-after-a-launch"></a>Anexar após uma inicialização
Depois que um programa é iniciado, a sessão de depuração está pronta para anexar o mecanismo DE depuração (DE) ao programa dito.

## <a name="design-decisions"></a>Decisões de design
 Como a comunicação é mais fácil dentro de um espaço de endereço compartilhado, você deve escolher entre duas abordagens de design: definir a comunicação entre a sessão de depuração e a DE. Ou então, defina a comunicação entre o e o programa. Escolha entre as seguintes opções:

- Se fizer mais sentido configurar a comunicação entre a sessão de depuração e a DE, a sessão de depuração cocriará o DE e solicitará que o DE seja anexado ao programa. Esse design deixa a sessão de depuração e outra em um espaço de endereço, e o ambiente e o programa de tempo de execução juntos em outra.

- Se fizer mais sentido configurar a comunicação entre o DE e o programa, o ambiente de tempo de execução cocriará o DE. Esse design deixa o SDM em um espaço de endereço e o DE, o ambiente DE tempo DE execução e o programa juntos em outro. Esse design é típico de um de que é implementado com um intérprete para executar linguagens com script.

    > [!NOTE]
    > Como o DE anexações ao programa depende da implementação. A comunicação entre o e o programa também depende da implementação.

## <a name="implementation"></a>Implementação
 Programaticamente, quando o SDM (Gerenciador de depuração de sessão) recebe primeiro o objeto [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa a ser iniciado, ele chama o método [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) , passando-o para um objeto [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) , que posteriormente é usado para passar eventos de depuração de volta para o SDM. `IDebugProgram2::Attach`Em seguida, o método chama o método [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) . Para obter mais informações sobre como o SDM recebe a `IDebugProgram2` interface, consulte [notificando a porta](../../extensibility/debugger/notifying-the-port.md).

 Se o seu precisar ser executado no mesmo espaço de endereço que o programa que você está Depurando: porque o DE é normalmente parte de um intérprete que está executando um script, o `IDebugProgramNodeAttach2::OnAttach` método retorna `S_FALSE` . O `S_FALSE` retorno indica que ele concluiu o processo de anexo.

 Se, no entanto, o DE é executado no espaço de endereço do SDM: o `IDebugProgramNodeAttach2::OnAttach` método retorna `S_OK` ou a interface [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) não é implementada no objeto [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) associado ao programa que você está depurando. Nesse caso, o método [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) é eventualmente chamado para concluir a operação de anexação.

 No último caso, você deve chamar o método [Getprogramid](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) no `IDebugProgram2` objeto que foi passado para o `IDebugEngine2::Attach` método, armazenar o `GUID` no objeto de programa local e retornar isso `GUID` quando o `IDebugProgram2::GetProgramId` método for chamado posteriormente neste objeto. O `GUID` é usado para identificar o programa exclusivamente em vários componentes de depuração.

 No caso do `IDebugProgramNodeAttach2::OnAttach` método `S_FALSE` que retorna, o `GUID` a ser usado para o programa é passado para esse método e é o `IDebugProgramNodeAttach2::OnAttach` método que define o `GUID` no objeto de programa local.

 O DE agora está anexado ao programa e pronto para enviar qualquer evento de inicialização.

## <a name="see-also"></a>Confira também
- [Anexando diretamente a um programa](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [Notificando a porta](../../extensibility/debugger/notifying-the-port.md)
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
