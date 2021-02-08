---
title: Entrando no modo de interrupção | Microsoft Docs
description: Saiba mais sobre o processo que ocorre para um ponto de interrupção encontrado em uma função, em execução na linha de código-fonte no cursor ou em execução em um ponto de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d3ec09994f6998f87daafc690b1908b31e54706b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99840646"
---
# <a name="enter-break-mode"></a>Entrar no modo de interrupção
As informações a seguir descrevem o processo que ocorre quando um ponto de interrupção é encontrado após a depuração em uma função, em execução na linha de código-fonte que tem o cursor em si ou em execução em um ponto de interrupção.

## <a name="break-mode-process"></a>Processo de modo de interrupção

1. O mecanismo DE depuração (DE) envia [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md), [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)ou qualquer outro evento de interrupção para fazer com que o IDE entre no modo de interrupção.

2. O SDM Obtém as informações da pilha de chamadas do thread, da seguinte maneira:

    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)

    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)

    - [IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) para obter as informações do código-fonte

    - [IDebugDocumentContext2:: GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md) obter o nome do arquivo

    - [IDebugDocumentContext2:: GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) para obter o intervalo de instruções

    - [IDebugStackFrame2:: GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) para obter informações de memória

## <a name="see-also"></a>Consulte também
- [Chamando eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
