---
description: Essa interface representa um tipo de enumeração.
title: IDebugEnumField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 18671f8f719dc797709677a14417eaa0a54aaea2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092521"
---
# <a name="idebugenumfield"></a>IDebugEnumField
Essa interface representa um tipo de enumeração.

## <a name="syntax"></a>Sintaxe

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um provedor de símbolo implementa essa interface para representar uma enumeração.

## <a name="notes-for-callers"></a>Observações para chamadores
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface da interface [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) se [getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) retornar `FIELD_TYPE_ENUM` .

## <a name="methods-in-vtable-order"></a>Métodos em ordem VTable
 Além dos métodos nas `IDebugField` `IDebugContainerField` interfaces e, essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|Retorna um [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que descreve o nome para esse tipo de enumeração.|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|Retorna o nome da constante de Enumeração associada ao valor especificado.|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|Retorna o valor associado ao nome constante de enumeração fornecido|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|Retorna o valor associado ao nome constante de enumeração fornecido, mas ignorando maiúsculas e minúsculas.|

## <a name="remarks"></a>Comentários
 É o símbolo subjacente que está realmente associado a um local com [BIND](../../../extensibility/debugger/reference/idebugbinder-bind.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [Associa](../../../extensibility/debugger/reference/idebugbinder-bind.md)
