---
description: Essa interface permite que um chamador determine se um fornecedor de porta pode preservar portas (gravando-as em disco) entre invocações do depurador e, em seguida, obter uma lista dessas portas preservadas.
title: IDebugPortSupplier3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa17984c9b7f3e87d4a7118188ecc6ca79c5deef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071929"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
Essa interface permite que um chamador determine se um fornecedor de porta pode preservar portas (gravando-as em disco) entre invocações do depurador e, em seguida, obter uma lista dessas portas preservadas.

## <a name="syntax"></a>Sintaxe

```
IDebugPortSupplier3 : IDebugPortSupplier2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface para dar suporte à persistência ou ao salvamento de informações de porta em disco. Essa interface deve ser implementada no mesmo objeto que a interface [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [QueryInterface](/cpp/atl/queryinterface) na `IDebugPortSupplier2` interface para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados da interface [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) , essa interface oferece suporte ao seguinte:

|Método|Descrição|
|------------|-----------------|
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|Retorna se o fornecedor da porta pode persistir portas (gravando-as no disco) entre invocações do depurador.|
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|Retorna um objeto que pode ser usado para enumerar por todas as portas que foram gravadas no disco por este fornecedor de porta.|

## <a name="remarks"></a>Comentários
 Se um fornecedor de porta pode persistir portas entre invocações, ele deve implementar essa interface. As portas devem ser carregadas quando o fornecedor da porta for instanciado e gravado no disco quando o fornecedor da porta for destruído.

 Um mecanismo de depuração normalmente não interage com um fornecedor de porta e não terá uso para essa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
