---
title: IDebugProgramNode2::Attach_V7 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ea09304d4481ed649f24985b3cabb2a6b1944311
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941627"
---
# <a name="idebugprogramnode2attachv7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> PRETERIDO. NÃO USE.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Attach_V7 (
   IDebugProgram2*       pMDMProgram,
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason
);
```

```csharp
int Attach_V7 (
   IDebugProgram2       pMDMProgram,
   IDebugEventCallback2 pCallback,
   uint                 dwReason
);
```

#### <a name="parameters"></a>Parâmetros

`pMDMProgram` [in] O [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) interface que representa o programa anexar.

 `pCallback` [in] O [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) interface a ser usada para enviar eventos de depuração para o SDM.

 `dwReason` [in] Um valor a partir de [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) enumeração que especifica o motivo para anexar.

## <a name="return-value"></a>Valor de retorno

Uma implementação deve retornar sempre `E_NOTIMPL`.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A partir do Visual Studio 2005, esse método não é mais usado e deve retornar sempre `E_NOTIMPL`. Consulte a [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) se o nó do programa deve indicar que ele não pode ser anexado a ou se o nó do programa é simplesmente definir o programa de interface para uma abordagem alternativa `GUID`. Caso contrário, implementar o [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) método.

## <a name="prior-to-visual-studio-2005"></a>Antes do Visual Studio 2005

Esse método precisa ser implementada somente se a Alemanha é executado no espaço de endereço do programa que está sendo depurado. Caso contrário, esse método deverá retornar `S_FALSE`.

Quando este método é chamado, o DE deve enviar o [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) objeto de evento, se ele já não tiver sido enviado para esta instância das [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) interface, bem como o [ IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) e [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) objetos de evento. O [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) objeto de evento é enviado se a `dwReason` parâmetro é `ATTACH_REASON_LAUNCH`.

O DE deve chamar o [GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) método na [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objeto fornecido pelo [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) eventos de objeto e deve armazenar o GUID do programa nos dados da instância para o `IDebugProgram2` objeto implementado por DE.

## <a name="see-also"></a>Consulte também

[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)  
[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)  
[Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)  
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)  
[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)  
[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)  
[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)  
[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)  
[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)  
[ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)