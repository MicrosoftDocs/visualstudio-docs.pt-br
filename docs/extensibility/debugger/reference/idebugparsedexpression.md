---
title: IDebugParsedExpression | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c5d0c7b32c6764c1911160f2909628f4102a9b96
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63413550"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Essa interface representa uma expressão analisada pronta para ser avaliada.

## <a name="syntax"></a>Sintaxe

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>Observações para implementadores
 Um avaliador de expressão implementa essa interface para representar uma expressão analisada que está pronta para avaliação.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) retorna essa interface.

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable
 A tabela a seguir mostra o método de `IDebugParsedExpression`.

|Método|Descrição|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|Avalia a expressão analisada.|

## <a name="remarks"></a>Comentários
 Quando o chamador está pronto para avaliar a expressão, ele chama [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) para retornar uma [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que contém o resultado da avaliação. Essa abordagem de duas partes para avaliação, análise e em seguida, avaliar, permite que a expressão analisada a ser avaliada várias vezes, ignorando o processo demorado de análise da expressão.

## <a name="requirements"></a>Requisitos
 Cabeçalho: ee.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)