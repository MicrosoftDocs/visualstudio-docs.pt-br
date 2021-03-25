---
description: A interface IDebugBreakpointRequest3 representa as informações necessárias para criar e associar qualquer tipo de ponto de interrupção.
title: IDebugBreakpointRequest3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6803b62975822f1b5219caa43844c8983303a998
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054407"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
Essa interface representa as informações necessárias para criar e associar qualquer tipo de ponto de interrupção. É uma extensão de [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md).

## <a name="syntax"></a>Sintaxe

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O SDM (Gerenciador de depuração de sessão) normalmente implementa essa interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O mecanismo de depuração (DE) acessa essa interface chamando [QueryInterface](/cpp/atl/queryinterface) na interface IDebugBreakpointRequest2 recebida em uma chamada para [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados de [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md), a `IDebugBreakpointRequest3` interface expõe o método a seguir.

|Método|Descrição|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|Obtém as informações de solicitação de ponto de interrupção que descrevem essa solicitação de ponto de interrupção.|

## <a name="remarks"></a>Comentários
 Essa interface é usada para fornecer informações adicionais para o por meio da estrutura de [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) . Essas informações adicionais incluem a ID do fornecedor DE DE (na forma de um GUID), o nome de um tracepoint e o nome de uma restrição de ponto de interrupção.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
