---
title: Arquitetura do avaliador de expressão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5ca1c7af9ee8a8a779cf238816125c0bc20199ca
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772697"
---
# <a name="expression-evaluator-architecture"></a>Arquitetura do avaliador de expressão
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Integrar uma linguagem de proprietária para o pacote de depuração do Visual Studio significa implementando as interfaces (EE) do avaliador de expressão necessária e chamar o provedor de símbolo de tempo de execução de linguagem comum (SP) e interfaces de associador. Os objetos de SP e associador, junto com o endereço de execução atual, são o contexto no qual as expressões são avaliadas. As informações de que essas interfaces produzem e consumam representam os principais conceitos da arquitetura de um EE.  
  
## <a name="overview"></a>Visão geral  
  
### <a name="parsing-the-expression"></a>Análise da expressão  
 Quando você estiver depurando um programa, as expressões são avaliadas por vários motivos, mas sempre quando o programa que está sendo depurado foi interrompido no ponto de interrupção (um ponto de interrupção colocado pelo usuário ou causada por uma exceção). É neste momento quando o Visual Studio obtém um quadro de pilha, conforme representado pela [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) interface do mecanismo de depuração (DES). Visual Studio, em seguida, chama [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter o [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) interface. Essa interface representa um contexto no qual as expressões podem ser avaliadas; [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) é o ponto de entrada para o processo de avaliação. Até este ponto, todas as interfaces são implementadas DE.  
  
 Quando `IDebugExpressionContext2::ParseText` é chamado, o DE instancia o EE associado com o idioma do arquivo de origem em que o ponto de interrupção ocorreu (o DE também instancia o SH neste momento). O EE é representado pela [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) interface. Em seguida, chama o DE [analisar](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para converter a expressão (na forma de texto) em uma expressão analisada, está pronto para avaliação. Essa expressão analisada é representado pela [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) interface. Observe que a expressão é analisada normalmente e não avaliada neste momento.  
  
 O DE cria um objeto que implementa o [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) interface, coloca o `IDebugParsedExpression` objeto para o `IDebugExpression2` objeto e retorna o `IDebugExpression2` do objeto de `IDebugExpressionContext2::ParseText`.  
  
### <a name="evaluating-the-expression"></a>Avaliação da expressão  
 Visual Studio chama o [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para avaliar a expressão analisada. Esses métodos chamam [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) (`IDebugExpression2::EvaluateSync` chama o método imediatamente, enquanto `IDebugExpression2::EvaluateAsync` chama o método por meio de um thread em segundo plano) para avaliar a expressão analisada e retornar um [ IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface que representa o valor e o tipo da expressão analisada. `IDebugParsedExpression::EvaluateSync` usa o SH, endereço e associador fornecidos para converter a expressão analisada em um valor real, representado pelo `IDebugProperty2` interface.  
  
### <a name="for-example"></a>Por exemplo  
 Depois que um ponto de interrupção é atingido em um programa em execução, o usuário opta por exibir uma variável na **QuickWatch** caixa de diálogo. Essa caixa de diálogo mostra o nome da variável, seu valor e seu tipo. O usuário geralmente pode alterar o valor.  
  
 Quando o **QuickWatch** caixa de diálogo é mostrada, o nome da variável que está sendo examinado é enviado como texto para [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md). Isso retorna um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto que representa a expressão analisada, nesse caso, a variável. [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) é chamado para produzir um `IDebugProperty2` objeto que representa o tipo e o valor da variável, bem como seu nome. É essa informação que é exibida.  
  
 Se o usuário altera o valor da variável, [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) é chamado com o novo valor, que altera o valor da variável na memória, portanto, ela será usada quando o programa retoma a execução.  
  
 Ver [exibindo locais](../../extensibility/debugger/displaying-locals.md) para obter mais detalhes sobre esse processo de exibir os valores das variáveis. Ver [alterando o valor de um Local](../../extensibility/debugger/changing-the-value-of-a-local.md) para obter mais detalhes sobre como o valor da variável é alterado.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contexto da avaliação](../../extensibility/debugger/evaluation-context.md)  
 Fornece os argumentos que são passados quando o DE chama o EE.  
  
 [Interfaces do principal avaliador de expressão](../../extensibility/debugger/key-expression-evaluator-interfaces.md)  
 Descreve as interfaces cruciais necessárias ao escrever um EE, junto com o contexto de avaliação.  
  
## <a name="see-also"></a>Consulte também  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [Exibir Locals](../../extensibility/debugger/displaying-locals.md)   
 [Alterar o valor de um Local](../../extensibility/debugger/changing-the-value-of-a-local.md)

