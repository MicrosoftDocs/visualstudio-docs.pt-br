---
description: Esta interface representa uma expressão analisada pronta para associação e avaliação.
title: IDebugExpression2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fe6a6955f5d8d4ae42d51e3623b0c4f966dc416
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152657"
---
# <a name="idebugexpression2"></a>IDebugExpression2
Esta interface representa uma expressão analisada pronta para associação e avaliação.

## <a name="syntax"></a>Sintaxe

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar uma expressão analisada pronta para ser avaliada.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) retorna essa interface. [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) retorna a interface [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) . Essas interfaces são acessíveis somente quando o programa que está sendo depurado tiver sido pausado e um quadro de pilha estiver disponível.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugExpression2` .

|Método|Descrição|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|Avalia essa expressão de forma assíncrona.|
|[Anular](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|Termina a avaliação de expressão assíncrona.|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|Avalia essa expressão de forma síncrona.|

## <a name="remarks"></a>Comentários
 Quando um programa é interrompido, o SDM (Gerenciador de depuração de sessão) Obtém um quadro de pilha do com uma chamada para [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md). O SDM então chama [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter a interface [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) . Isso é seguido por uma chamada para [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para criar a `IDebugExpression2` interface, que representa a expressão analisada pronta para ser avaliada.

 O SDM chama [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para realmente avaliar a expressão e produzir um valor.

 Em uma implementação do `IDebugExpressionContext2::ParseText` , o de usa a função do com `CoCreateInstance` para criar uma instância de um avaliador de expressão e obter uma interface [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) (consulte o exemplo na `IDebugExpressionEvaluator` interface). O DE então chama [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para obter uma interface [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) . Essa interface é usada na implementação de `IDebugExpression2::EvaluateSync` e `IDebugExpression2::EvaluateAsync` para executar a avaliação.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
