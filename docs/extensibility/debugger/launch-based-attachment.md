---
title: Anexo baseado em inicialização | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4910a97350366500b56593ec0076fdf0990b6d8f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738464"
---
# <a name="launch-based-attachment"></a>Anexo baseado em inicialização
O anexo baseado em inicialização em um programa é automático. Quando o processo que hospeda o programa é iniciado pelo SDM, o anexo baseado em inicialização segue um caminho semelhante ao do método de anexo manual. Para obter informações, consulte [anexar ao programa](../../extensibility/debugger/attaching-to-the-program.md).

## <a name="the-attaching-process"></a>O processo de anexação
 A principal diferença é a sequência de eventos após a chamada de **anexação** , da seguinte maneira:

1. Envie um objeto de evento **IDebugEngineCreateEvent2** para o SDM. Para obter detalhes, consulte [enviar eventos](../../extensibility/debugger/sending-events.md).

2. Chame o `IDebugProgram2::GetProgramId` método na interface **IDebugProgram2** passada para o método **Attach** .

3. Envie um objeto de evento **IDebugProgramCreateEvent2** para notificar o SDM de que o objeto **IDebugProgram2** local foi criado para representar o programa para o de.

4. Envie um objeto de evento [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) para notificar o SDM de que um novo thread é criado para o processo iniciado.

## <a name="see-also"></a>Confira também
- [Enviar os eventos necessários](../../extensibility/debugger/sending-the-required-events.md)
- [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
