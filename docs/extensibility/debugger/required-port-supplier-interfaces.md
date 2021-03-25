---
title: Interfaces de fornecedor de porta necessárias | Microsoft Docs
description: Saiba mais sobre as interfaces que um fornecedor de porta deve executar. Um fornecedor de porta fornece portas e as implementa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f5755ce47a2b76c9a0d38b1f7eed3b38d64c876
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070603"
---
# <a name="required-port-supplier-interfaces"></a>Interfaces de fornecedor de porta necessárias
Um fornecedor de porta deve implementar a interface [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) . [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 Um fornecedor de porta fornece portas e as implementa. Portanto, ele deve executar as seguintes interfaces:

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  Descreve a porta e enumera todos os processos em execução na porta.

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  Fornece para iniciar e encerrar processos na porta.

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  Fornece um mecanismo para programas em execução dentro do contexto dessa porta para notificá-lo da criação e destruição de nós de programa. Para obter mais informações, consulte [nós de programa](../../extensibility/debugger/program-nodes.md).

- `IConnectionPointContainer`

  Fornece um ponto de conexão para [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md).

## <a name="port-supplier-operation"></a>Operação de fornecedor de porta
 O coletor [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md) recebe notificações quando processos e programas são criados e destruídos em uma porta. Uma porta é necessária para enviar [IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md) quando um processo é criado e [IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) quando um processo é destruído na porta. Uma porta também é necessária para enviar [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) quando um programa é criado e [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) quando um programa é destruído em um processo em execução na porta.

 Normalmente, uma porta envia eventos de criação e destruição de programas em resposta aos métodos [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) e [RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) , respectivamente.

 Como uma porta pode iniciar e encerrar processos físicos e programas lógicos, as seguintes interfaces também devem ser implementadas pelo mecanismo de depuração:

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)

  Descreve o processo físico. Pelo menos os seguintes métodos devem ser implementados:

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)

  - [GetProcessId](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)

  Fornece uma maneira para o SDM se anexar e se desconectar de um processo.

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)

  Descreve o programa lógico. Pelo menos os seguintes métodos devem ser implementados:

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)

  - [GetProcess](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)

- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)

  Fornece uma maneira para o SDM ser anexado a este programa.

## <a name="see-also"></a>Confira também
- [Implementando um fornecedor de porta](../../extensibility/debugger/implementing-a-port-supplier.md)
