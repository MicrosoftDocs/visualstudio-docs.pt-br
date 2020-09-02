---
title: IEnumDebugPorts2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3cc46ef8abb6ef1fbb8f072d97b0fc4a537af1a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716107"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
Essa interface enumera as portas de um fornecedor de máquina ou porta.

## <a name="syntax"></a>Syntax

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface para representar uma lista de portas criadas pelo fornecedor. O Visual Studio implementa essa interface para dar suporte ao seu próprio fornecedor de porta.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) para obter essa interface representando uma lista de portas criadas pelo fornecedor da porta. Chame [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md) para obter essa interface representando uma lista de portas que foram salvas em disco.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IEnumDebugPorts2` .

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|Recupera um número especificado de portas em uma sequência de enumeração.|
|[Ignorar](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|Ignora um número especificado de portas em uma sequência de enumeração.|
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[Clone](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|Obtém o número de portas em um enumerador.|

## <a name="remarks"></a>Comentários
 O Visual Studio usa essa interface para ajudar a preencher uma lista de portas usadas para anexar a processos.

 Um mecanismo de depuração normalmente não usa essa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Principais interfaces](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
