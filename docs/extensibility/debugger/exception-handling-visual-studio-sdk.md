---
title: Tratamento de exceção (SDK do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o processo que ocorre quando as exceções são geradas. Este artigo descreve todas as etapas envolvidas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f74337964b73683a71b180699da626121a4d3067
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097013"
---
# <a name="exception-handling-visual-studio-sdk"></a>Tratamento de exceção (SDK do Visual Studio)
O seguinte descreve o processo que ocorre quando as exceções são geradas.

## <a name="exception-handling-process"></a>Processo de tratamento de exceção

1. Quando uma exceção é lançada pela primeira vez, mas antes de ser manipulada pelo manipulador de exceção no programa que está sendo depurado, o mecanismo de depuração (DE) envia um [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) para o SDM (Gerenciador de depuração de sessão) como um evento de parada. O `IDebugExceptionEvent2` será enviado se apenas as configurações da exceção (especificado na caixa de diálogo exceções no pacote de depuração) especificarem que o usuário deseja parar em notificações de exceção de primeira chance.

2. O SDM chama [IDebugExceptionEvent2:: getexcept](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) para obter a propriedade de exceção.

3. O pacote de depuração chama [IDebugExceptionEvent2:: CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) para determinar quais opções apresentar ao usuário.

4. O pacote de depuração solicita ao usuário como tratar a exceção abrindo uma caixa de diálogo de exceção de primeira chance.

5. Se o usuário optar por continuar, o SDM chamará [IDebugExceptionEvent2:: CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md).

    - Se o método retornar S_OK, o chamará [IDebugExceptionEvent2::P asstodebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md).

         – ou –

         Se o método retornar S_FALSE, o programa que está sendo depurado receberá uma segunda chance de manipular a exceção.

6. Se o programa que está sendo depurado não tiver nenhum manipulador para uma exceção de segunda chance, o DE enviará um `IDebugExceptionEvent2` para o SDM como **EVENT_SYNC_STOP**.

7. O pacote de depuração solicita ao usuário como tratar a exceção abrindo uma caixa de diálogo de exceção de primeira chance.

8. O pacote de depuração chama [IDebugExceptionEvent2:: CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) para determinar quais opções apresentar ao usuário.

9. O pacote de depuração solicita ao usuário como tratar a exceção abrindo uma caixa de diálogo de exceção de segunda chance.

10. Se o método retornar S_OK, chama `IDebugExceptionEvent2::PassToDebuggee` .

## <a name="see-also"></a>Confira também
- [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
