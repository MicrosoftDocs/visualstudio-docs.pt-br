---
title: Avaliar uma expressão da janela Inspeção | Microsoft Docs
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
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4dc9a56927ebe1e7b962ab815eb34028ba75350c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801453"
---
# <a name="evaluating-a-watch-window-expression"></a>Avaliando uma expressão da janela Inspeção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Quando a execução pausa, o Visual Studio chama o mecanismo de depuração (DE) para determinar o valor atual de cada expressão em sua lista de inspeção. O DE avalia cada expressão usando um avaliador de expressão (EE) e seu valor no Visual Studio exibe a **inspeção** janela.  
  
 Aqui está uma visão geral de como uma expressão de lista de inspeção é avaliada:  
  
1.  Visual Studio chama o DE [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) para obter um contexto de expressão que pode ser usado para avaliar expressões.  
  
2.  Para cada expressão na lista de monitoramento, o Visual Studio chama [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) para converter o texto da expressão em uma expressão analisada.  
  
3.  `IDebugExpressionContext2::ParseText` chamadas [analisar](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) para fazer o trabalho real de analisar o texto e produzem uma [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) objeto.  
  
4.  `IDebugExpressionContext2::ParseText` cria uma [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto e coloca o `IDebugParsedExpression` objeto nele. Este eu`DebugExpression2` objeto, em seguida, é retornado para o Visual Studio.  
  
5.  Chamadas do Visual Studio [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para avaliar a expressão analisada.  
  
6.  `IDebugExpression2::EvaluateSync` passará a chamada para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) para fazer a avaliação real e produzir uma [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto que é retornado para o Visual Studio.  
  
7.  Chamadas do Visual Studio [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) para obter o valor da expressão que é exibido na lista de inspeção.  
  
## <a name="parse-then-evaluate"></a>Analisar e avaliar  
 Uma vez que uma expressão complexa de análise pode levar muito mais que avaliá-lo, o processo de avaliação de uma expressão é dividido em duas etapas: 1) analisar a expressão e 2) avaliar a expressão analisada. Dessa forma, a avaliação pode ocorrer várias vezes, mas a expressão precisa ser analisado apenas uma vez. A expressão analisada intermediária é retornada do EE em um [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) objeto que é encapsulado por sua vez e retornado de como um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto. O `IDebugExpression` objeto adia a avaliação de todas as para o `IDebugParsedExpression` objeto.  
  
> [!NOTE]
>  Não é necessário para um EE aderir a esse processo em duas etapas, mesmo que o Visual Studio pressupõe que isso. o EE pode analisar e avaliar na mesma etapa quando [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) é chamado (Isso é como o exemplo MyCEE funciona, por exemplo). Se sua linguagem pode formar expressões complexas, você talvez queira separar a etapa de análise da etapa de avaliação. Isso pode aumentar o desempenho no depurador do Visual Studio quando muitas expressões de inspeção estão sendo mostradas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exemplo de implementação da Avaliação de expressão](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)  
 Usa o exemplo de MyCEE para percorrer o processo de avaliação da expressão.  
  
 [Avaliar uma expressão de Inspeção](../../extensibility/debugger/evaluating-a-watch-expression.md)  
 Explica o que acontece após uma análise da expressão com êxito.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Contexto da avaliação](../../extensibility/debugger/evaluation-context.md)  
 Fornece os argumentos que são passados quando o mecanismo de depuração (DES) chama o avaliador de expressão (EE).  
  
## <a name="see-also"></a>Consulte também  
 [Escrevendo um avaliador de expressão do CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

