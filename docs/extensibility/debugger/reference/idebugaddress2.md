---
description: Essa interface fornece acesso à ID do processo que possui o objeto cujo endereço é representado por essa interface.
title: IDebugAddress2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58a3f01472f60996b7094334de8cb2dbd79acac0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143955"
---
# <a name="idebugaddress2"></a>IDebugAddress2
Essa interface fornece acesso à ID do processo que possui o objeto cujo endereço é representado por essa interface.

## <a name="syntax"></a>Sintaxe

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um provedor de símbolo implementa essa interface no mesmo objeto que implementa a interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) . Essa interface fornece acesso à ID do processo que possui o objeto que está relacionado a esse endereço.

## <a name="notes-for-callers"></a>Observações para chamadores
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface da interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados da interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) , essa interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|Recupera a ID do processo que possui o objeto representado por essa interface.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
