---
title: Processos | Microsoft Docs
description: Este artigo descreve a definição e a função de um processo na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f3cadf314b189c72320da3f54488af8560cf3fd8
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901247"
---
# <a name="processes"></a>Processos
Na arquitetura do depurador, um *processo*:

- É um contêiner para um conjunto de programas. Ele é muito análogo a um processo do Windows, que é um contêiner para um conjunto de threads.

- Pode se identificar por nome, identificador ou identificador físico.

- Pode enumerar todos os programas em execução (e seus threads).

- Pode descrever a si mesmo, a porta em que está sendo executado e o computador que a contém.

- Pode criar um ou mais programas, encerrar qualquer um dos programas que ele cria ou fazer com que um programa pare.

- É representado por uma interface [IDebugProcess2,](../../extensibility/debugger/reference/idebugprocess2.md) que é criada quando o processo é lançado. Um processo é lançado pelo SDM (gerenciador de depuração de sessão) [ou launchSuspended.](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)

  O pacote de depuração pode anexar um DE (mecanismo de depuração) a um processo chamando [Anexar](../../extensibility/debugger/reference/idebugprocess2-attach.md), o que significa que o DE é anexado a todos os programas possíveis em execução no processo que ele pode manipular. Por exemplo, se a DE do Common Language Runtime for anexada a um processo, ela será anexada somente a programas que executam código gerenciado.

## <a name="see-also"></a>Confira também
- [Programas](../../extensibility/debugger/programs.md)
- [Threads](../../extensibility/debugger/threads.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [Depurar pacote](../../extensibility/debugger/debug-package.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)
