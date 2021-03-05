---
description: Essa interface representa bytes de memória.
title: IDebugMemoryBytes2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1c6f1cf03aa36a4ae6c935d1efc8970ce3ff5f7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165079"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
Essa interface representa bytes de memória.

## <a name="syntax"></a>Sintaxe

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar bytes na memória.

## <a name="notes-for-callers"></a>Observações para chamadores
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) retorna essa interface para fornecer acesso à memória do sistema. [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) e [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md) retornam essa interface para fornecer acesso aos bytes de um objeto.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugMemoryBytes2` .

|Método|Descrição|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|Lê uma sequência de bytes, começando em um determinado local.|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|Grava `dwCount` bytes, começando em `pStartContext` .|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|Obtém o tamanho, em bytes, da memória representada por essa interface.|

## <a name="remarks"></a>Comentários
 Para propriedades, uma interface [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que representa uma matriz fornece uma `IDebugMemoryBytes2` interface para acessar os valores nessa matriz.

 A exibição de **memória** do Visual Studio chama [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) para recuperar uma `IDebugMemoryBytes2` interface para acessar a memória do sistema. O endereço a ser acessado é obtido analisando a expressão inserida como um endereço na exibição de memória e, em seguida, avaliando a expressão analisada usando [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para obter uma `IDebugProperty2` interface. Uma chamada para [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) retorna o [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) que descreve o endereço de memória. Esse contexto de memória é passado para [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) e [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
