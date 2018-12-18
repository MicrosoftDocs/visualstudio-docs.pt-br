---
title: IDebugEngine2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e2cfe7e2f54b45ecfe8fdb34943b87818a13feab
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31113088"
---
# <a name="idebugengine2"></a>IDebugEngine2
Essa interface representa um mecanismo de depuração (DE). Ele é usado para gerenciar vários aspectos de uma sessão de depuração, da criação de pontos de interrupção para configuração e limpar exceções.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEngine2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada por um DE personalizados para gerenciar a depuração de programas. Esta interface deve ser implementada por DE.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é chamada pelo Gerenciador de depuração (SDM) para gerenciar a sessão de depuração, incluindo gerenciamento de exceções, criando pontos de interrupção e responder a eventos síncronos enviados por DE sessão.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugEngine2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|Cria um enumerador para todos os programas que estão sendo depurado por um DE.|  
|[Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)|Anexa um DE um programa.|  
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|Cria um ponto de interrupção pendente DE.|  
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|Especifica como o DE deve tratar uma exceção especificada.|  
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|Remove a exceção especificada para que ele não é tratado pelo mecanismo de depuração.|  
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|Remove a lista de exceções que definiu o IDE para um idioma ou a arquitetura de tempo de execução específica.|  
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|Obtém o GUID DE.|  
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|Informa a DE que o programa especificado foi encerrado atypically e que o DE deve limpar todas as referências para o programa e enviar um programa destruir o evento.|  
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|Chamado pelo SDM para indicar que um evento de depuração síncrona, anteriormente enviado por DE para SDM, foi recebido e processado.|  
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|Define a localidade de.|  
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|Define a raiz do registro atualmente em uso por DE.|  
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|Define uma métrica.|  
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|Solicitações que todos os programas que estão sendo depurados por este DE parar a execução da próxima vez que um dos seus threads de tentativas de execução.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)