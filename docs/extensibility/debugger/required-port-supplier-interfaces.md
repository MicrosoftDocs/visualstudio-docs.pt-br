---
title: As Interfaces de fornecedor porta necessárias | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1c727cb39b480d72a3e0aa2083ca795bb65ac0ff
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39252408"
---
# <a name="required-port-supplier-interfaces"></a>Interfaces de fornecedor porta necessárias
Um fornecedor de porta deve implementar o [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) interface.[ IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)  
  
 Um fornecedor de porta fornece portas e implementá-las. Portanto, ele deve executar as seguintes interfaces:  
  
-   [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)  
  
     Descreve a porta e enumera todos os processos em execução na porta.  
  
-   [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)  
  
     Fornece para iniciar e encerrar processos na porta.  
  
-   [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)  
  
     Fornece um mecanismo para programas em execução dentro do contexto desta porta para notificá-lo de destruição e criação de nó do programa. Para obter mais informações, consulte [nós de programa](../../extensibility/debugger/program-nodes.md).  
  
-   `IConnectionPointContainer`  
  
     Fornece um ponto de conexão para [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md).  
  
## <a name="port-supplier-operation"></a>Operação de fornecedor de porta  
 O [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md) coletor recebe notificações quando o processo e os programas são criados e destruídos em uma porta. Uma porta é necessário para enviar [IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md) quando um processo é criado e [IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) quando um processo for destruído na porta. Uma porta também é necessário para enviar [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) quando um programa é criado e [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) quando um programa for destruído em um processo em execução na porta.  
  
 Uma porta normalmente programa envia criar e destruir eventos em resposta para o [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) e [RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) métodos, respectivamente.  
  
 Como uma porta pode iniciar e encerrar processos físicos e lógicos programas, as interfaces a seguir também devem ser implementadas pelo mecanismo de depuração:  
  
-   [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)  
  
     Descreve o processo de física. Pelo menos os seguintes métodos devem ser implementados:  
  
    -   [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)  
  
    -   [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)  
  
    -   [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)  
  
    -   [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)  
  
    -   [GetProcessId](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)  
  
    -   [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)  
  
-   [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)  
  
     Fornece uma maneira para o SDM anexar e desanexar um processo em si.  
  
-   [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)  
  
     Descreve a lógica do programa. Pelo menos os seguintes métodos devem ser implementados:  
  
    -   [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)  
  
    -   [GetProcess](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)  
  
    -   [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)  
  
-   [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)  
  
     Fornece uma maneira para o SDM anexar a este programa.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando um fornecedor de porta](../../extensibility/debugger/implementing-a-port-supplier.md)