---
description: Essa interface representa uma posição no espaço de endereço do computador que está executando o programa que está sendo depurado.
title: IDebugMemoryContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a967c992fc55065c50dbbe173495e7c1199df59
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058476"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
Essa interface representa uma posição no espaço de endereço do computador que está executando o programa que está sendo depurado.

## <a name="syntax"></a>Sintaxe

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar um endereço na memória.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) ou [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md) retorna essa interface. Além disso, as chamadas para [Adicionar](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md) e [subtrair](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md) retornam novas cópias dessa interface após a aplicação da operação aritmética apropriada.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugMemoryContext2` .

|Método|Descrição|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|Obtém o nome da exibição do usuário para este contexto.|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|Obtém informações que descrevem esse contexto.|
|[Adicionar](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|Adiciona um valor especificado ao endereço do contexto atual para criar um novo contexto.|
|[Subtrair](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|Subtrai um valor especificado do endereço do contexto atual para criar um novo contexto.|
|[Comparar](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|Compara dois contextos da maneira indicada por sinalizadores de comparação.|

## <a name="remarks"></a>Comentários
 A janela de **memória** do Visual Studio chama [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) para obter a `IDebugMemoryContext2` interface que contém a expressão avaliada usada para o endereço de memória. Esse contexto é passado para [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) e [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md) para especificar o endereço a ser lido ou gravado.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)
