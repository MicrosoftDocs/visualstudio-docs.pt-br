---
title: Criando um ponto de interrupção | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, creating
- debugging [Debugging SDK], creating breakpoints
ms.assetid: 6f9f87bb-192e-45e0-9a7a-ffe729e87f7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f89b99f15374ef7e0bbc6964ee1ff521eeb469f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903621"
---
# <a name="create-a-breakpoint"></a>Criar um ponto de interrupção
Veja a seguir uma descrição do processo de criação de um ponto de interrupção.

## <a name="methods-in-breakpoint-creation"></a>Métodos na criação de ponto de interrupção
 Quando o módulo necessário para associar um ponto de interrupção é carregado, o SDM (Session Debug Manager) chama os seguintes métodos:

1. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)

2. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)

3. [IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)

    > [!NOTE]
    > **Canbind** é chamado somente quando um usuário faz um ponto de interrupção da janela **pontos de interrupção** .

4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

5. [IDebugPendingBreakpoint2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)

## <a name="see-also"></a>Confira também
- [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
