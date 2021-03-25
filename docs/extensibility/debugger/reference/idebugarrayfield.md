---
description: Esta interface descreve um tipo ou símbolo de matriz.
title: IDebugArrayField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 073438a99531b278a148b6eb19ff6e5af88004e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058931"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
Esta interface descreve um tipo ou símbolo de matriz.

## <a name="syntax"></a>Sintaxe

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O provedor de símbolos implementa essa interface no mesmo objeto que implementa a interface [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) . Essa interface é uma especialização que representa objetos de matriz.

## <a name="notes-for-callers"></a>Observações para chamadores
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface da interface [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) se [getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) retornar o sinalizador `FIELD_TYPE_ARRAY` .

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos nas interfaces [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) e [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) , essa interface implementa o seguinte:

|Método|Descrição|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|Obtém o número de elementos na matriz.|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|Obtém o tipo de elemento na matriz.|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|Obtém a classificação da matriz.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
