---
title: Anexando ao programa | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00b9780d0d302b9e067feed057d1a8d49c5f9fc0
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903213"
---
# <a name="attach-to-the-program"></a>Anexar ao programa
Depois de registrar seus programas com a porta apropriada, você deve anexar o depurador ao programa que deseja depurar.

## <a name="choose-how-to-attach"></a>Escolha como anexar
 Há três maneiras pelas quais o SDM (Session Debug Manager) tenta anexar ao programa que está sendo depurado.

1. Para programas que são iniciados pelo mecanismo de depuração por meio do método [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) (típico de linguagens interpretadas, por exemplo), o SDM Obtém a interface [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) do objeto [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) associado ao programa ao qual está sendo anexado. Se o SDM puder obter a `IDebugProgramNodeAttach2` interface, o SDM chamará o método [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) . O `IDebugProgramNodeAttach2::OnAttach` método retorna `S_OK` para indicar que ele não foi anexado ao programa e que outras tentativas podem ser feitas para anexar ao programa.

2. Se o SDM puder obter a interface [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md) do programa que está sendo anexado, o SDM chamará o método [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md) . Essa abordagem é típica para programas que foram iniciados remotamente pelo fornecedor de porta.

3. Se o programa não puder ser anexado por meio dos `IDebugProgramNodeAttach2::OnAttach` `IDebugProgramEx2::Attach` métodos ou, o SDM carregará o mecanismo de depuração (se ainda não tiver sido carregado) chamando a `CoCreateInstance` função e, em seguida, chamará o método [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) . Essa abordagem é típica para programas iniciados localmente por um fornecedor de porta.

    Também é possível que um fornecedor de porta personalizado chame o `IDebugEngine2::Attach` método na implementação do fornecedor da porta personalizada do `IDebugProgramEx2::Attach` método. Normalmente, nesse caso, o fornecedor de porta personalizada inicia o mecanismo de depuração no computador remoto.

   O anexo é obtido quando o SDM (Gerenciador de depuração de sessão) chama o método [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) .

   Se você executar o DE no mesmo processo que o aplicativo a ser depurado, deverá implementar os seguintes métodos de [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md):

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  Depois que o `IDebugEngine2::Attach` método for chamado, siga estas etapas em sua implementação do `IDebugEngine2::Attach` método:

1. Envie um objeto de evento [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) para o SDM. Para obter mais informações, consulte [enviando eventos](../../extensibility/debugger/sending-events.md).

2. Chame o método [Getprogramid](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) no objeto [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) que foi passado para o `IDebugEngine2::Attach` método.

     Isso retorna um `GUID` que é usado para identificar o programa. O `GUID` deve ser armazenado no objeto que representa o programa local para de e deve ser retornado quando o `IDebugProgram2::GetProgramId` método é chamado na `IDebugProgram2` interface.

    > [!NOTE]
    > Se você implementar a `IDebugProgramNodeAttach2` interface, o programa `GUID` será passado para o `IDebugProgramNodeAttach2::OnAttach` método. Isso `GUID` é usado para o programa `GUID` retornado pelo `IDebugProgram2::GetProgramId` método.

3. Envie um objeto de evento [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) para notificar o SDM de que o `IDebugProgram2` objeto local foi criado para representar o programa para o de. Para obter detalhes, consulte [enviando eventos](../../extensibility/debugger/sending-events.md).

    > [!NOTE]
    > Esse não é o mesmo `IDebugProgram2` objeto que foi passado para o `IDebugEngine2::Attach` método. O objeto passado anteriormente `IDebugProgram2` é reconhecido pela porta apenas e é um objeto separado.

## <a name="see-also"></a>Confira também
- [Anexo baseado em inicialização](../../extensibility/debugger/launch-based-attachment.md)
- [Enviando eventos](../../extensibility/debugger/sending-events.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)
- [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
