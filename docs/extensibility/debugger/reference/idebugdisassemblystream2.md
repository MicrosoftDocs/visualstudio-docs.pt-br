---
description: Essa interface representa um fluxo de instruções.
title: IDebugDisassemblyStream2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 760d77ced3cc07da2dd02c21cf3ed0200df14231
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166561"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
Essa interface representa um fluxo de instruções.

## <a name="syntax"></a>Sintaxe

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um mecanismo de depuração implementa essa interface para dar suporte à desmontagem do código de um programa.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para o método [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md) retorna essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugDisassemblyStream2` .

|Método|Descrição|
|------------|-----------------|
|[Ler](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|Lê as instruções a partir da posição atual no fluxo de desmontagem.|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|Move o ponteiro de leitura no fluxo de desmontagem de um determinado número de instruções relativas a uma posição especificada.|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|Retorna um identificador de local de código para um contexto de código específico.|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|Retorna um objeto de contexto de código correspondente a um identificador de local de código especificado.|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|Retorna um identificador de local de código que representa o local do código atual.|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|Obtém o documento de origem associado a este fluxo de desmontagem.|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|Obtém o escopo deste fluxo de desmontagem.|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|Obtém o tamanho desse fluxo de desmontagem.|

## <a name="remarks"></a>Comentários
 O fluxo de desmontagem pode ser criado para representar o espaço de endereço inteiro ou apenas uma função ou um módulo dentro do espaço. Cada instrução é representada por uma estrutura [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) retornada por uma chamada para o método [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
