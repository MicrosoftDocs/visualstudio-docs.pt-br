---
description: Essa interface representa uma posição abstrata de uma função em um documento de origem.
title: IDebugFunctionPosition2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2
helpviewer_keywords:
- IDebugFunctionPosition2 interface
ms.assetid: a835f65b-91b0-48ad-8485-04534c814b1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5afd44827d8d9b6f244bc914728bd090261ab25
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063468"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
Essa interface representa uma posição abstrata de uma função em um documento de origem.

## <a name="syntax"></a>Sintaxe

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar a posição de uma função dentro de um documento de origem.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é fornecida como parte de uma União de [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) (especificamente, uma estrutura de [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) ) que, por sua vez, faz parte da estrutura de [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) , usada na criação de um ponto de interrupção pendente.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugFunctionPosition2` .

|Método|Descrição|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|Obtém o nome da função à qual essa posição é relativa.|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|Obtém o deslocamento do início da função.|

## <a name="remarks"></a>Comentários
 A posição representada por essa interface é baseada em texto, especificamente, uma estrutura [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
