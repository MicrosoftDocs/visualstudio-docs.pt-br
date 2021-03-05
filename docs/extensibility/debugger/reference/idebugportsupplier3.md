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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8db7c2321d5a309f66b85a3f177e20cb3f9b1244
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150387"
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
