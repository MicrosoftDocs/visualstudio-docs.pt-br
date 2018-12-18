---
title: IDebugProgram2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 392d9bd350d6207e6725c31c659a6edf1518a807
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31122594"
---
# <a name="idebugprogram2"></a>IDebugProgram2
Essa interface representa um programa que está em execução em um processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProgram2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) e um fornecedor de porta personalizada implementam essa interface para representar um programa em um processo. O Gerenciador de sessão de depuração (SDM) também implementa essa interface para fornecer informações para [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md).  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) evento retorna essa interface para um novo programa. Essa interface também é usada como um parâmetro para muitos métodos em várias interfaces.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugProgram2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|Enumera os threads que estão em execução deste programa.|  
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|Obtém o nome do programa.|  
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|Obtém o que este programa está sendo executado no processo.|  
|[Encerrar](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|Encerra o programa.|  
|[Anexar](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|Anexa a este programa.|  
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|Determina se um mecanismo de depuração (DE) poderá desanexar do programa.|  
|[Desanexar](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|Desanexa o depurador deste programa.|  
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|Obtém um identificador globalmente exclusivo para este programa.|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|Obtém propriedades do programa.|  
|[Executar](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|Continua executando esse programa de um estado parado. Qualquer estado de execução anterior está desmarcado.|  
|[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|Continua executando esse programa de um estado parado. Qualquer estado de execução anterior é preservado.|  
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|Executa uma etapa.|  
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|Solicitações que este programa interromper a execução na próxima vez um de seu código é executado de threads.|  
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|Obtém o nome e o identificador do mecanismo de depuração (DE) executando esse programa.|  
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|Enumera os contextos de código para uma determinada posição em um arquivo de origem.|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|Obtém os bytes de memória para este programa.|  
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|Obtém o fluxo de desmontagem para este programa ou a parte desse programa.|  
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|Enumera os módulos que esse programa foi carregado e está em execução.|  
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|Obtém a atualização de editar e continuar (c) para este programa.<br /><br /> Um mecanismo de depuração personalizado não implementa esse método (sempre deve retornar `E_NOTIMPL`).|  
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|Enumera os caminhos de código deste programa.|  
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|Grava um despejo de memória em um arquivo.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="remarks"></a>Comentários  
 Um programa é um contêiner de thread em execução em uma arquitetura de tempo de execução específica, enquanto um processo é composto de um ou mais programas.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)   
 [Avançar](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)   
 [Evento](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)   
 [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)