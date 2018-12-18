---
title: Anexar após uma inicialização | Microsoft Docs
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
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 416c05a7592d9f036a76a5d96537b4be917a0651
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774699"
---
# <a name="attaching-after-a-launch"></a>Anexando após uma inicialização
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Depois que um programa tiver sido iniciado, a sessão de depuração está pronta para anexar o mecanismo de depuração (DE) para esse programa.  
  
## <a name="design-decisions"></a>Decisões de design  
 Porque a comunicação é mais fácil dentro de um espaço de endereço compartilhado, você deve decidir se faz mais sentido para facilitar a comunicação entre a sessão de depuração e o DE ou entre a Alemanha e o programa. Escolha entre os seguintes:  
  
-   Se faz mais sentido para facilitar a comunicação entre a sessão de depuração e o DE, a sessão de depuração cria conjunta DE e solicita que o DE anexar ao programa. Isso deixa a sessão de depuração e DE juntos em um espaço de endereço e o ambiente de tempo de execução e o programa juntos em outro.  
  
-   Se faz mais sentido para facilitar a comunicação entre a Alemanha e o programa, o ambiente de tempo de execução conjunta cria o DE. Isso deixa o SDM em um espaço de endereço, Alemanha, o ambiente de tempo de execução e o programa juntos em outro. Isso é típico de a DE que é implementada com um interpretador executar linguagens de script.  
  
    > [!NOTE]
    >  Como o DE anexa ao programa é dependente de implementação. Comunicação entre a Alemanha e o programa também é dependente da implementação.  
  
## <a name="implementation"></a>Implementação  
 Programaticamente, quando o Gerenciador de sessão de depuração (SDM) recebe primeiro a [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) o objeto que representa o programa a ser iniciado, ele chama o [anexar](../../extensibility/debugger/reference/idebugprogram2-attach.md) método, passando-lhe um [ IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) objeto, que é posteriormente usado para passar eventos de depuração de volta para o SDM. O `IDebugProgram2::Attach` , em seguida, chama um método de [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) método. Para obter mais informações sobre como o SDM recebe o `IDebugProgram2` interface, consulte [notificar a porta](../../extensibility/debugger/notifying-the-port.md).  
  
 Se seu Alemanha precisa ser executado no mesmo espaço de endereço que o programa que está sendo depurado, normalmente porque o DE faz parte de um interpretador executando um script, o `IDebugProgramNodeAttach2::OnAttach` método retorna `S_FALSE`, indicando que ela foi concluída com o processo de anexação.  
  
 Se, por outro lado, a Alemanha é executado no espaço de endereço do SDM, o `IDebugProgramNodeAttach2::OnAttach` retorn `S_OK` ou o [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) interface não é implementada pelo tudo no [IDebugProgramNode2 ](../../extensibility/debugger/reference/idebugprogramnode2.md) objeto associado ao programa que está sendo depurado. Nesse caso, o [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) método eventualmente é chamado para concluir a operação de anexação.  
  
 No último caso, você deve chamar o [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) método na `IDebugProgram2` objeto que foi passado para o `IDebugEngine2::Attach` método, o repositório a `GUID` no programa de local de objeto e retornar esse `GUID` quando o `IDebugProgram2::GetProgramId` método é chamado posteriormente neste objeto. O `GUID` é usado para identificar o programa exclusivamente entre os vários componentes de depuração.  
  
 Observe que no caso do `IDebugProgramNodeAttach2::OnAttach` método retornando `S_FALSE`, o `GUID` a ser usado para o programa é passado ao método e é o `IDebugProgramNodeAttach2::OnAttach` método que define o `GUID` no objeto de local do programa.  
  
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

