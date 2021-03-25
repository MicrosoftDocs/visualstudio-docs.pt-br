---
description: Esta interface representa uma expressão analisada pronta para ser avaliada.
title: IDebugParsedExpression | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 00daeac20d621657d61aa802d79a46a3ee0e7aa7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084578"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Esta interface representa uma expressão analisada pronta para ser avaliada.

## <a name="syntax"></a>Sintaxe

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um avaliador de expressão implementa essa interface para representar uma expressão analisada que está pronta para avaliação.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) retorna essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra o método de `IDebugParsedExpression` .

|Método|Descrição|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|Avalia a expressão analisada.|

## <a name="remarks"></a>Comentários
 Quando o chamador está pronto para avaliar a expressão, ele chama [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) para retornar um [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que contém o resultado da avaliação. Essa abordagem de duas partes para avaliação, análise, avaliação, permite que a expressão analisada seja avaliada várias vezes, ignorando o processo demorado de análise da expressão.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
