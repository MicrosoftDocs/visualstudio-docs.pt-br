---
description: Essa interface permite que o SDM (Gerenciador de depuração de sessão) se conecte a um programa e obtenha o nó de programa associado a um programa.
title: IDebugProgramEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e39a469d04ac14f3ed36366d035bf4ca01a9d2ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087321"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
Essa interface permite que o SDM (Gerenciador de depuração de sessão) se conecte a um programa e obtenha o nó de programa associado a um programa.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface no mesmo objeto que a interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) para permitir que o SDM anexe a um programa enquanto, ao mesmo tempo, permite que o fornecedor de porta acompanhe todas as sessões anexadas ao programa. O fornecedor da porta personalizada pode implementar essa interface se escolher.

## <a name="notes-for-callers"></a>Observações para chamadores
 O SDM chama [QueryInterface](/cpp/atl/queryinterface) em uma `IDebugProgram2` interface para obter essa interface para controlar as sessões que foram anexadas a programas.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProgramEx2` .

|Método|Descrição|
|------------|-----------------|
|[Attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|Anexa um programa a uma sessão.|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|Obtém o nó de programa associado a um programa.|

## <a name="remarks"></a>Comentários
 Essa interface é privada entre o SDM e o programa.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Portpriv. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
