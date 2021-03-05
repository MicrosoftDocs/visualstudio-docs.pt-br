---
description: Essa interface representa um mecanismo DE depuração (DE).
title: IDebugEngine2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce76ccdc444dafc4b6b8ee6afb3c9ded8adcf3d0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153827"
---
# <a name="idebugengine2"></a>IDebugEngine2
Essa interface representa um mecanismo DE depuração (DE). Ele é usado para gerenciar vários aspectos de uma sessão de depuração, desde a criação de pontos de interrupção até a configuração e a limpeza de exceções.

## <a name="syntax"></a>Sintaxe

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por um DE um DE para gerenciar a depuração de programas. Essa interface deve ser implementada pelo DE.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é chamada pelo SDM (Gerenciador de depuração de sessão) para gerenciar a sessão de depuração, incluindo o gerenciamento de exceções, a criação de pontos de interrupção e a resposta a eventos síncronos enviados pelo.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugEngine2` .

|Método|Descrição|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|Cria um enumerador para todos os programas que estão sendo depurados por um DE.|
|[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)|Anexa um DE DE um programa.|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|Cria um ponto de interrupção pendente no DE.|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|Especifica como o DE deve tratar uma determinada exceção.|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|Remove a exceção especificada para que ela não seja mais manipulada pelo mecanismo de depuração.|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|Remove a lista de exceções que o IDE definiu para uma arquitetura ou idioma de tempo de execução específico.|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|Obtém o GUID de DE.|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|Informa um DE que o programa especificado foi encerrado atypically e que o DE deve limpar todas as referências ao programa e enviar um evento de destruição de programa.|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|Chamado pelo SDM para indicar que um evento DE depuração síncrono, enviado anteriormente pelo DE para o SDM, foi recebido e processado.|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|Define a localidade de DE.|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|Define a raiz do registro atualmente em uso pelo DE.|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|Define uma métrica.|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|Solicita que todos os programas que estão sendo depurados por essa execução interrompam a próxima vez que um de seus threads tentarem ser executados.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
