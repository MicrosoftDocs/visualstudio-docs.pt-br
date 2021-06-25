---
title: Contexto de avaliação | Microsoft Docs
description: 'Quando o mecanismo de depuração chama o avaliador de expressão, os argumentos determinam o contexto para localizar e avaliar símbolos: pSymbolProvider, pAddress e pBinder.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6c3ab6fe53ad288089dc88587e06547573d80cb9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898572"
---
# <a name="evaluation-context"></a>Contexto de avaliação
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte Avaliadores de expressão CLR e Exemplo de [avaliador](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) [de expressão gerenciada.](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

 Quando o DE (mecanismo de depuração) chama o avaliador de expressão (EE), três argumentos que são passados para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) determinam o contexto para localizar e avaliar símbolos, conforme mostrado na tabela a seguir.

## <a name="arguments"></a>Argumentos

|Argumento|Descrição|
|--------------|-----------------|
|`pSymbolProvider`|Uma interface [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) que especifica o sh (manipulador de símbolos) a ser usado para identificar o símbolo.|
|`pAddress`|Uma [interface IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) que especifica o ponto de execução atual. Essa interface localiza o método que contém o código que está sendo executado.|
|`pBinder`|Uma interface [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) que localiza o valor e o tipo de um símbolo, considerando seu nome.|

 `IDebugParsedExpression::EvaluateSync` retorna uma [interface IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa o valor resultante e seu tipo.

## <a name="see-also"></a>Confira também
- [Interfaces do avaliador de expressão-chave](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
