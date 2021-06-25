---
title: Interfaces principais do avaliador de expressão | Microsoft Docs
description: Saiba mais sobre as interfaces com as quais você deve estar familiarizado ao escrever um avaliador de expressão, juntamente com o contexto de avaliação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: abfa4018e763bbbac5ff788f401d0ceb76eb97a1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901260"
---
# <a name="key-expression-evaluator-interfaces"></a>Interfaces principais do avaliador de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Ao escrever um avaliador de expressão (EE), juntamente com o contexto de avaliação, você deve estar familiarizado com as interfaces a seguir.

## <a name="interface-descriptions"></a>Descrições de interface

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     Tem um único método, [GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md), que obtém uma estrutura de dados que representa o ponto atual de execução. Essa estrutura de dados é um dos três argumentos que o mecanismo de depuração (DE) passa para o método [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) para avaliar uma expressão. Normalmente, essa interface é implementada pelo provedor de símbolos.

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     Tem o método [BIND](../../extensibility/debugger/reference/idebugbinder-bind.md) , que obtém a área de memória que contém o valor atual de um símbolo. Considerando o método recipiente, representado por um objeto [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) , e o próprio símbolo, representado por um objeto [IDebugField](../../extensibility/debugger/reference/idebugfield.md) , `IDebugBinder::Bind` retorna o valor do símbolo. `IDebugBinder` normalmente é implementado pelo DE.

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     Representa um tipo de dados simples. Para tipos mais complexos, como matrizes e métodos, use as interfaces [IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md) e [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) derivadas, respectivamente. [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) é outra interface derivada importante que representa os símbolos que contêm outros símbolos, como métodos ou classes. A `IDebugField` interface (e seus derivados) normalmente é implementada pelo provedor de símbolos.

     Um `IDebugField` objeto pode ser usado para localizar o nome e o tipo de um símbolo e, junto com um objeto [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) , pode ser usado para localizar seu valor.

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     Representa os bits reais do valor de tempo de execução de um símbolo. A [ligação](../../extensibility/debugger/reference/idebugbinder-bind.md) usa um objeto [IDebugField](../../extensibility/debugger/reference/idebugfield.md) , que representa um símbolo e retorna um objeto [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) . O método [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md) retorna o valor do símbolo em um buffer de memória. Normalmente, um DE implementa essa interface para representar o valor de uma propriedade na memória.

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     Essa interface representa o próprio avaliador de expressão. O método de chave é [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md), que retorna uma interface [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) .

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     Esta interface representa uma expressão analisada pronta para ser avaliada. O método de chave é [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) que retorna um IDebugProperty2 que representa o valor e o tipo da expressão.

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     Essa interface representa um valor e seu tipo e é o resultado de uma avaliação de expressão.

## <a name="see-also"></a>Confira também
- [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md)
