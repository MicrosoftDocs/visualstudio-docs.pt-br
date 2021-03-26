---
title: Avaliação de expressão (Visual Studio Debugging SDK) | Microsoft Docs
description: Durante o modo de interrupção, o IDE avalia as expressões que envolvem variáveis de programa. Saiba como o mecanismo de depuração analisa e avalia uma expressão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9e6a79a3268f0bd4acebde795109d39466032a2f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096792"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>Avaliação de expressão (SDK de depuração do Visual Studio)
Durante o modo de interrupção, o IDE deve avaliar expressões simples envolvendo várias variáveis de programa. Para realizar sua avaliação, o mecanismo DE depuração (DE) deve analisar e avaliar uma expressão que é inserida em uma das janelas do IDE.

 As expressões são criadas com o método [IDebugExpressionContext2::P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) e representadas pela interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) resultante.

 A interface **IDebugExpression2** é implementada pelo de e chama seu método **EvalAsync** para retornar uma interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) para o IDE, a fim de exibir os resultados da avaliação da expressão no IDE. [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) retorna uma estrutura que é usada para colocar o valor de uma expressão em uma janela **Watch** ou na janela **locais** .

 O pacote de depuração ou o SDM (Gerenciador de depuração de sessão) chama [IDebugExpression2:: EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) ou [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para obter uma interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa o resultado da avaliação. `IDebugProperty2` tem métodos que retornam o nome, o tipo e o valor da expressão. Essas informações aparecem em várias janelas do depurador.

## <a name="using-expression-evaluation"></a>Usando a avaliação de expressão
 Para usar a avaliação de expressão, você deve implementar o método [IDebugExpressionContext2::P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) e todos os métodos da interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) , conforme mostrado na tabela a seguir.

|Método|Descrição|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|Avalia uma expressão de forma assíncrona.|
|[Anular](../../extensibility/debugger/reference/idebugexpression2-abort.md)|Termina a avaliação de expressão assíncrona.|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|Avalia uma expressão de forma síncrona.|

 A avaliação síncrona e assíncrona exige a implementação do método [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) . A avaliação de expressões assíncronas requer a implementação de [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md).

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
