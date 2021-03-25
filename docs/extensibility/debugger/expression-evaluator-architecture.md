---
title: Arquitetura do avaliador de expressão | Microsoft Docs
description: Saiba mais sobre como integrar uma linguagem proprietária ao pacote de depuração do Visual Studio, incluindo o avaliador de expressão e interfaces de provedor/associador de símbolo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 31b382f4765a115657fb213f39530e88e4008c95
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094725"
---
# <a name="expression-evaluator-architecture"></a>Arquitetura do avaliador de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 A integração de um idioma proprietário ao pacote de depuração do Visual Studio significa que você deve configurar as interfaces do avaliador de expressão (EE) necessárias e chamar o provedor de símbolo de tempo de execução de linguagem comum (SP) e as interfaces do fichário. Os objetos SP e Binder, juntamente com o endereço de execução atual, são o contexto no qual as expressões são avaliadas. As informações que essas interfaces produzem e consomem representam os principais conceitos da arquitetura de um EE.

## <a name="overview"></a>Visão geral

### <a name="parse-the-expression"></a>Analisar a expressão
 Quando você estiver depurando um programa, as expressões serão avaliadas por vários motivos, mas sempre quando o programa que está sendo depurado tiver sido interrompido em um ponto de interrupção (um ponto de interrupção colocado pelo usuário ou um causado por uma exceção). Nesse momento, o Visual Studio Obtém um registro de ativação, conforme representado pela interface [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) , do mecanismo de depuração (de). Em seguida, o Visual Studio chama [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter a interface [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) . Essa interface representa um contexto no qual as expressões podem ser avaliadas; [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) é o ponto de entrada para o processo de avaliação. Até esse ponto, todas as interfaces são implementadas pelo DE.

 Quando `IDebugExpressionContext2::ParseText` é chamado, o de instancia o EE associado ao idioma do arquivo de origem em que o ponto de interrupção ocorreu (o de também instancia o sh neste ponto). O EE é representado pela interface [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) . O DE então chama [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para converter a expressão (na forma de texto) em uma expressão analisada, pronta para avaliação. Essa expressão analisada é representada pela interface [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) . A expressão é normalmente analisada e não avaliada neste ponto.

 O DE cria um objeto que implementa a interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) , coloca o `IDebugParsedExpression` objeto no `IDebugExpression2` objeto e retorna o `IDebugExpression2` objeto de `IDebugExpressionContext2::ParseText` .

### <a name="evaluate-the-expression"></a>Avaliar a expressão
 O Visual Studio chama [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para avaliar a expressão analisada. Ambos os métodos chamam [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) ( `IDebugExpression2::EvaluateSync` chama o método imediatamente, enquanto `IDebugExpression2::EvaluateAsync` chama o método por meio de um thread em segundo plano) para avaliar a expressão analisada e retornar uma interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa o valor e o tipo da expressão analisada. `IDebugParsedExpression::EvaluateSync` usa o SH, o endereço e o associado fornecidos para converter a expressão analisada em um valor real, representado pela `IDebugProperty2` interface.

### <a name="for-example"></a>Por exemplo
 Depois que um ponto de interrupção é atingido em um programa em execução, o usuário escolhe exibir uma variável na caixa de diálogo **QuickWatch** . Essa caixa de diálogo mostra o nome da variável, seu valor e seu tipo. Normalmente, o usuário pode alterar o valor.

 Quando a caixa de diálogo **QuickWatch** é mostrada, o nome da variável que está sendo examinada é enviado como texto para [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md). Isso retorna um objeto [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) que representa a expressão analisada, nesse caso, a variável. Em seguida, [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) é chamado para produzir um `IDebugProperty2` objeto que representa o valor e o tipo da variável, bem como seu nome. São essas informações exibidas.

 Se o usuário alterar o valor da variável, [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) será chamado com o novo valor, que altera o valor da variável na memória para que ela seja usada quando o programa retomar a execução.

 Consulte [exibindo locais](../../extensibility/debugger/displaying-locals.md) para obter mais detalhes sobre esse processo de exibição dos valores de variáveis. Consulte [alterando o valor de um local](../../extensibility/debugger/changing-the-value-of-a-local.md) para obter mais detalhes sobre como o valor de uma variável é alterado.

## <a name="in-this-section"></a>Nesta seção
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md) Fornece os argumentos que são passados quando o DE chama o EE.

 [Interfaces principais do avaliador de expressão](../../extensibility/debugger/key-expression-evaluator-interfaces.md) Descreve as interfaces cruciais necessárias ao escrever um EE, juntamente com o contexto de avaliação.

## <a name="see-also"></a>Confira também
- [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)
- [Alterando o valor de um local](../../extensibility/debugger/changing-the-value-of-a-local.md)
