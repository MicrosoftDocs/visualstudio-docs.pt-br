---
title: Contexto de avaliação | Microsoft Docs
description: 'Quando o mecanismo de depuração chama o avaliador de expressão, os argumentos determinam o contexto para localizar e avaliar símbolos: pSymbolProvider, pAddress e pBinder.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ccfc921f8175a92b0a082798ce8ccc44990d2e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096974"
---
# <a name="evaluation-context"></a>Contexto de avaliação
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Quando o mecanismo de depuração (DE) chama o avaliador de expressão (EE), três argumentos que são passados para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) determinam o contexto para localizar e avaliar símbolos, conforme mostrado na tabela a seguir.

## <a name="arguments"></a>Argumentos

|Argumento|Descrição|
|--------------|-----------------|
|`pSymbolProvider`|Uma interface [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) que especifica o manipulador de símbolo (SH) a ser usado para identificar o símbolo.|
|`pAddress`|Uma interface [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) que especifica o ponto de execução atual. Essa interface localiza o método que contém o código que está sendo executado.|
|`pBinder`|Uma interface [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) que localiza o valor e o tipo de um símbolo, dado seu nome.|

 `IDebugParsedExpression::EvaluateSync` Retorna uma interface [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa o valor resultante e seu tipo.

## <a name="see-also"></a>Confira também
- [Interfaces principais do avaliador de expressão](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
