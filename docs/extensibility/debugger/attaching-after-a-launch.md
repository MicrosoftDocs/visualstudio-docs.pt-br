---
title: Anexar após uma inicialização | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b767ef1aeed691255a62a9cb5c1e264034acf24e
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39152900"
---
# <a name="attach-after-a-launch"></a>Anexar após uma inicialização
Depois que um programa for iniciado, a sessão de depuração está pronta para anexar o mecanismo de depuração (DE) para esse programa.  
  
## <a name="design-decisions"></a>Decisões de design  
 Porque a comunicação é mais fácil dentro de um espaço de endereço compartilhado, você deve escolher entre duas abordagens de design: definir a comunicação entre a sessão de depuração e o DE. Ou então, defina a comunicação entre a Alemanha e o programa. Escolha entre os seguintes:  
  
-   Se faz mais sentido para configurar a comunicação entre a sessão de depuração e o DE, a sessão de depuração cria conjunta DE e solicita que o DE anexar ao programa. Esse design deixa a sessão de depuração e DE juntos em um espaço de endereço e o ambiente de tempo de execução e o programa juntos em outro.  
  
-   Se faz mais sentido para configurar a comunicação entre a Alemanha e o programa, o ambiente de tempo de execução cria conjunta DE. Esse design deixa o SDM em um espaço de endereço DE, o ambiente de tempo de execução e o programa juntos em outro. Esse design é típico de a DE que é implementada com um interpretador executar linguagens de script.  
  
    > [!NOTE]
    >  Como o DE anexa ao programa é dependente de implementação. Comunicação entre a Alemanha e o programa também é dependente da implementação.  
  
## <a name="implementation"></a>Implementação  
 Programaticamente, quando o Gerenciador de sessão de depuração (SDM) recebe primeiro a [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) o objeto que representa o programa a ser iniciado, ele chama o [anexar](../../extensibility/debugger/reference/idebugprogram2-attach.md) método, passando-lhe um [ IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) objeto, que é posteriormente usado para passar eventos de depuração de volta para o SDM. O `IDebugProgram2::Attach` , em seguida, chama um método de [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) método. Para obter mais informações sobre como o SDM recebe o `IDebugProgram2` interface, consulte [notificar a porta](../../extensibility/debugger/notifying-the-port.md).  
  
 Se seu Alemanha precisa ser executado no mesmo espaço de endereço como o programa de depuração: como o DE normalmente é parte de um interpretador de que está executando um script, o `IDebugProgramNodeAttach2::OnAttach` retorno do método `S_FALSE`. O `S_FALSE` retorno indica que ele concluir o processo de anexação.  
  
 Se, no entanto, o DE será executado no espaço de endereço do SDM: o `IDebugProgramNodeAttach2::OnAttach` retorn `S_OK`, ou o [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) interface não é implementada pelo tudo no [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) objeto associado com o programa que você está depurando. Nesse caso, o [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) método eventualmente é chamado para concluir a operação de anexação.  
  
 No último caso, você deve chamar o [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) método na `IDebugProgram2` objeto que foi passado para o `IDebugEngine2::Attach` método, o repositório a `GUID` no programa de local de objeto e retornar esse `GUID` quando o `IDebugProgram2::GetProgramId` método é chamado posteriormente neste objeto. O `GUID` é usado para identificar o programa exclusivamente entre os vários componentes de depuração.  
  
 No caso do `IDebugProgramNodeAttach2::OnAttach` método retornando `S_FALSE`, o `GUID` a ser usado para o programa é passado ao método e é o `IDebugProgramNodeAttach2::OnAttach` método que define o `GUID` no objeto de local do programa.  
  
 O DE agora está anexado ao programa e pronto para enviar os eventos de inicialização.  
  
## <a name="see-also"></a>Consulte também  
 [Anexar diretamente a um programa](../../extensibility/debugger/attaching-directly-to-a-program.md)   
 [Notificar a porta](../../extensibility/debugger/notifying-the-port.md)   
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)   
 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [Anexar](../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [Anexar](../../extensibility/debugger/reference/idebugengine2-attach.md)