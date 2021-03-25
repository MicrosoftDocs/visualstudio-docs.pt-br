---
title: 'IDebugProgramNode2:: Attach_V7 | Microsoft Docs'
description: Esse método de interface é um método de anexo antigo e preterido usado antes do Visual Studio 2005.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c949bba45457917e4dd00bdc05bc300f3a38eb7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053588"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> Preterido. NÃO USE.

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

## <a name="parameters"></a>Parâmetros

`pMDMProgram`\
no A interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa ao qual anexar.

`pCallback`\
no A interface [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) a ser usada para enviar eventos de depuração para o SDM.

`dwReason`\
no Um valor da enumeração [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) que especifica o motivo da anexação.

## <a name="return-value"></a>Valor Retornado

Uma implementação sempre deve retornar `E_NOTIMPL` .

## <a name="remarks"></a>Comentários

> [!WARNING]
> A partir do Visual Studio 2005, esse método não é mais usado e sempre deve retornar `E_NOTIMPL` . Consulte a interface [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) para obter uma abordagem alternativa se o nó do programa precisar indicar que ele não pode ser anexado a ou se o nó do programa estiver simplesmente definindo o programa `GUID` . Caso contrário, implemente o método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) .

## <a name="prior-to-visual-studio-2005"></a>Antes do Visual Studio 2005

Esse método precisa ser implementado somente se o DE for executado no espaço de endereço do programa que está sendo depurado. Caso contrário, esse método deve retornar `S_FALSE` .

Quando esse método é chamado, o DE deve enviar o objeto de evento [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) , se ele ainda não tiver sido enviado para essa instância da interface [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) , bem como os objetos de evento [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) e [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) . O objeto de evento [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) será enviado se o `dwReason` parâmetro for `ATTACH_REASON_LAUNCH` .

O DE deve chamar o método [Getprogramid](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) no objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) fornecido pelo objeto de evento [IDEBUGPROGRAMCREATEEVENT2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) e deve armazenar o GUID do programa nos dados da instância para o `IDebugProgram2` objeto implementado pelo de.

## <a name="see-also"></a>Confira também

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
