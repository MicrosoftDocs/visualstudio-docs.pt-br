---
title: IDebugProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c79ec83adcb766bd7c6de3d31a2ae790710a838
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348963"
---
# <a name="idebugprogram2"></a>IDebugProgram2
Essa interface representa um programa que está em execução em um processo.

## <a name="syntax"></a>Sintaxe

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>Observações para implementadores
 O mecanismo de depuração (DE) e um fornecedor de porta personalizado implementam essa interface para representar um programa em um processo. O Gerenciador de sessão de depuração (SDM) também implementa essa interface para fornecer informações em [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md).

## <a name="notes-for-callers"></a>Observações para chamadores
 O [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) evento retorna essa interface para um novo programa. Essa interface também é usada como um parâmetro para muitos métodos em várias interfaces.

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable
 A tabela a seguir mostra os métodos de `IDebugProgram2`.

|Método|Descrição|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|Enumera os threads que estão executando nesse programa.|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|Obtém o nome do programa.|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|Obtém o que este programa está em execução no processo.|
|[Terminar](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|Finaliza este programa.|
|[Anexar](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|Anexa a este programa.|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|Determina se um mecanismo de depuração (DES) poderá desanexar do programa.|
|[Desanexar](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|Desanexa o depurador deste programa.|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|Obtém um identificador global exclusivo para este programa.|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|Obtém as propriedades do programa.|
|[Executar](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|Continua a execução deste programa de um estado parado. Qualquer estado de execução anterior está desmarcado.|
|[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|Continua a execução deste programa de um estado parado. Qualquer estado de execução anterior é preservado.|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|Executa uma etapa.|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|Solicitações que este programa parar a execução na próxima hora em que um dos seu código de execuções de threads.|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|Obtém o nome e o identificador do mecanismo de depuração (DES) executar este programa.|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|Enumera os contextos de código para uma posição especificada em um arquivo de origem.|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|Obtém os bytes de memória para este programa.|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|Obtém o fluxo de desmontagem para este programa ou a parte deste programa.|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|Enumera os módulos que este programa foi carregado e está em execução.|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|Obtém a atualização de editar e continuar (ENC) para este programa.<br /><br /> Um mecanismo de depuração personalizado não implementa esse método (ele deve sempre retornar `E_NOTIMPL`).|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|Enumera os caminhos de código deste programa.|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|Grava um despejo de um arquivo.|

## <a name="requirements"></a>Requisitos
 Header: msdbg.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Comentários
 Um programa é um contêiner de thread em execução em uma arquitetura de tempo de execução específica, enquanto um processo é composto por um ou mais programas.

## <a name="see-also"></a>Consulte também
- [Principais interfaces](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [Avançar](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)