---
title: IDebugExpressionContext2 | Microsoft Docs
description: Essa interface representa um contexto para a avaliação da expressão
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6d8745207f1ab075aedd43815e7a97a4f0721bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092287"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
Essa interface representa um contexto para avaliação de expressão.

## <a name="syntax"></a>Sintaxe

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar um contexto no qual uma expressão pode ser avaliada.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) retorna a interface this. Essa interface é acessível somente quando o programa que está sendo depurado tiver sido pausado e um quadro de pilha estiver disponível.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugExpressionContext2` .

|Método|Descrição|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|Recupera o nome do contexto de avaliação.|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|Analisa uma expressão baseada em texto para avaliação.|

## <a name="remarks"></a>Comentários
 Um contexto de avaliação pode ser considerado como um escopo para executar a avaliação da expressão.

 Quando um programa é interrompido, o SDM (Gerenciador de depuração de sessão) Obtém um quadro de pilha do com uma chamada para [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md). O SDM então chama [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter a `IDebugExpressionContext2` interface. Isso é seguido por uma chamada para [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para criar uma interface [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) , que representa a expressão analisada pronta para ser avaliada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
