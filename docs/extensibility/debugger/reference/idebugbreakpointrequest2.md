---
description: A interface IDebugBreakPointRequest2 representa as informações necessárias para criar e associar qualquer tipo de ponto de interrupção.
title: IDebugBreakpointRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e7d13c945de1358265a5eb92769192ce736be49
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162349"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
Essa interface representa as informações necessárias para criar e associar qualquer tipo de ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O SDM (Gerenciador de depuração de sessão) normalmente implementa essa interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O mecanismo de depuração (DE) recebe essa interface por meio de uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) para criar um ponto de interrupção pendente. Uma chamada para [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) pode recuperar essa interface a partir de de.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugBreakpointRequest2` .

|Método|Descrição|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|Obtém o tipo de local do ponto de interrupção dessa solicitação de ponto de interrupção.|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|Obtém as informações de solicitação de ponto de interrupção que descrevem essa solicitação de ponto de interrupção.|

## <a name="remarks"></a>Comentários
 Depois que o programa que está sendo depurado tiver sido carregado, uma chamada para [BIND](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) associará um ponto de interrupção pendente ao local solicitado no programa.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [Associa](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
