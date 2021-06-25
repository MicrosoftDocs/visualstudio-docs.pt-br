---
title: Anexo baseado em lançamento | Microsoft Docs
description: Saiba mais sobre o anexo baseado em lançamento para um programa, que é automático e segue um caminho como o do anexo manual.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 97bbc098e766a1025c372ff35c5849bfe652649f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904328"
---
# <a name="launch-based-attachment"></a>Anexo baseado em lançamento
O anexo baseado em lançamento para um programa é automático. Quando o processo que hospeda o programa é lançado pelo SDM, o anexo baseado em lançamento segue um caminho semelhante ao do método de anexo manual. Para obter informações, [consulte Anexar ao programa](../../extensibility/debugger/attaching-to-the-program.md).

## <a name="the-attaching-process"></a>O processo de anexação
 A principal diferença é a sequência de eventos após a **chamada Anexar,** da seguinte forma:

1. Envie um **objeto de evento IDebugEngineCreateEvent2** para o SDM. Para obter detalhes, consulte [Enviar eventos](../../extensibility/debugger/sending-events.md).

2. Chame o `IDebugProgram2::GetProgramId` método na interface **IDebugProgram2** passado para o **método Attach.**

3. Envie um objeto de evento **IDebugProgramCreateEvent2** para notificar o SDM de que o objeto **IDebugProgram2** local foi criado para representar o programa para a DE.

4. Envie um objeto de evento [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) para notificar o SDM de que um novo thread é criado para o processo que foi lançado.

## <a name="see-also"></a>Confira também
- [Enviar os eventos necessários](../../extensibility/debugger/sending-the-required-events.md)
- [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
