---
description: Essa interface representa uma lista de caminhos de código.
title: IEnumCodePaths2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e8ff8b4532ab67a969c8270eeb83bdf715e0b1c0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091728"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
Essa interface representa uma lista de caminhos de código.

## <a name="syntax"></a>Sintaxe

```
IEnumCodePaths2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar uma lista de caminhos de código.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md) para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IEnumCodePaths2` .

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|Recupera um número especificado de caminhos de código em uma sequência de enumeração.|
|[Skip](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|Ignora um número especificado de caminhos de código em uma sequência de enumeração.|
|[Redefinir](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[8i](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|Obtém o número de caminhos de código em um enumerador.|

## <a name="remarks"></a>Comentários
 Um caminho de código representa um ponto de ramificação ou uma chamada de função em um programa. Uma lista de caminhos de código representa o caminho por meio do qual a execução do código foi realizada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
