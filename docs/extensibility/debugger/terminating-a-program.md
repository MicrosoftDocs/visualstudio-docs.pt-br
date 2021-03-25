---
title: Encerrando um programa | Microsoft Docs
description: Este artigo descreve como o IDE usa o mecanismo de depuração para encerrar um único programa com um único thread.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: db67e0a391f40fc17a80e616e10aa46a600337a4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057852"
---
# <a name="terminating-a-program"></a>Finalizando um programa
A seção a seguir descreve o encerramento de um único programa com um thread.

## <a name="termination-process"></a>Processo de encerramento

1. O DE envia um [IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) com um [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)válido.

2. O DE envia um [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) com um [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)válido.

   O IDE entra no modo de design. O mecanismo de depuração ou o ambiente de tempo de execução chama [IDebugPortNotify2:: RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) para remover o programa da porta.

## <a name="see-also"></a>Confira também
- [Chamando eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
