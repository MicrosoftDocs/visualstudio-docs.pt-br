---
description: Essa interface representa um programa que está sendo executado em um processo.
title: IDebugProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f6effa250749f448ed1a02c4b7a699d50b7388e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084396"
---
# <a name="idebugprogram2"></a>IDebugProgram2
Essa interface representa um programa que está sendo executado em um processo.

## <a name="syntax"></a>Sintaxe

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) e um fornecedor de porta personalizado implementam essa interface para representar um programa em um processo. O SDM (Gerenciador de depuração de sessão) também implementa essa interface para fornecer informações a serem [anexadas](../../../extensibility/debugger/reference/idebugprogram2-attach.md).

## <a name="notes-for-callers"></a>Observações para chamadores
 O evento [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) retorna essa interface para um novo programa. Essa interface também é usada como um parâmetro para muitos métodos em várias interfaces.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProgram2` .

|Método|Descrição|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|Enumera os threads que estão em execução neste programa.|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|Obtém o nome do programa.|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|Obtém o processo em que este programa está sendo executado.|
|[Encerrar](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|Encerra este programa.|
|[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|Anexa a este programa.|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|Determina se um mecanismo DE depuração (DE) pode ser desanexado do programa.|
|[Desanexar](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|Desanexa o depurador deste programa.|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|Obtém um identificador global exclusivo para este programa.|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|Obtém as propriedades do programa.|
|[Executar](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|Continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior é limpo.|
|[Continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|Continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior é preservado.|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|Executa uma etapa.|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|Solicita que este programa interrompa a execução na próxima vez que um de seus threads executar o código.|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|Obtém o nome e o identificador do mecanismo de depuração (DE) que executa este programa.|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|Enumera os contextos de código para uma determinada posição em um arquivo de origem.|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|Obtém os bytes de memória para este programa.|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|Obtém o fluxo de desmontagem deste programa ou parte deste programa.|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|Enumera os módulos que este programa carregou e está executando.|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|Obtém a atualização do ENC (editar e continuar) para este programa.<br /><br /> Um mecanismo de depuração personalizado não implementa esse método (ele sempre deve retornar `E_NOTIMPL` ).|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|Enumera os caminhos de código deste programa.|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|Grava um despejo em um arquivo.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Comentários
 Um programa é um contêiner de threads em execução em uma arquitetura de tempo de execução específica, enquanto um processo é composto de um ou mais programas.

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Evento](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
