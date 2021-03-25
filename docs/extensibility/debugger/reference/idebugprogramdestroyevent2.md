---
description: Essa interface é enviada pelo mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando um programa é executado até a conclusão.
title: IDebugProgramDestroyEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramDestroyEvent2
helpviewer_keywords:
- IDebugProgramDestroyEvent2
ms.assetid: ddf127ca-c4a5-4071-90ca-68faf2f57dbd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 49242ea2c0116ae57f1c063bf3d5fe5e1db2ce17
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084370"
---
# <a name="idebugprogramdestroyevent2"></a>IDebugProgramDestroyEvent2
Essa interface é enviada pelo mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando um programa é executado até a conclusão.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O ou o fornecedor de porta personalizada implementa essa interface para relatar que um programa foi encerrado e não está mais disponível para depuração. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O fornecedor DE porta Personalizada cria e envia esse objeto de evento para relatar o encerramento de um programa. O DE envia esse evento usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado. O fornecedor da porta personalizada envia esse evento usando a interface [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) .

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra o método de `IDebugProgramDestroyEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetExitCode](../../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)|Obtém o código de saída do programa.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
