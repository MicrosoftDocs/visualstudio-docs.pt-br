---
title: IDebugEngineProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e5ccf2327e660a983bcb3032363a92ac8a6f71d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730303"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
Essa interface fornece suporte para depuração multi-threaded.

## <a name="syntax"></a>Syntax

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um mecanismo de depuração implementa essa interface para dar suporte à depuração simultânea de vários threads. Essa interface é implementada no mesmo objeto que implementa a interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface de uma `IDebugProgram2` interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugEngineProgram2` .

|Método|Descrição|
|------------|-----------------|
|[Parar](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|Interrompe todos os threads em execução neste programa.|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|Inspeciona a execução (ou pare de observar a execução) para ocorrer no thread determinado.|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|Permite que a avaliação de expressão (ou não permite) ocorra no thread determinado, mesmo que o programa seja interrompido.|

## <a name="remarks"></a>Comentários
 O Visual Studio chama essa interface em resposta a um evento [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) e para definir os Estados "inspecionar a etapa de thread" e "inspecionar a avaliação da expressão no thread" do programa. [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) é chamado sempre que o programa é interrompido; Esse método dá ao programa a oportunidade de encerrar todos os threads.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
