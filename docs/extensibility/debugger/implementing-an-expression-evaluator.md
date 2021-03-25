---
title: Implementando um avaliador de expressão | Microsoft Docs
description: Saiba mais sobre como avaliar uma expressão, que envolve o mecanismo de depuração, o provedor de símbolos, o objeto de fichário e o avaliador de expressão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7caee7b58f77f1b4e3f120f27ae076b438bedc63
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059867"
---
# <a name="implement-an-expression-evaluator"></a>Implementar um avaliador de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Avaliar uma expressão é uma interatividade complexa entre o mecanismo DE depuração (DE), o provedor de símbolos (SP), o objeto de fichário e o avaliador de expressão (EE). Esses quatro componentes são conectados por interfaces que são implementadas por um componente e consumidas por outro.

 O EE usa uma expressão de de na forma de uma cadeia de caracteres e a analisa ou avalia. O EE executa as seguintes interfaces, que são consumidas pelo:

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  O EE chama o objeto Binder, fornecido pelo DE, para obter o valor de símbolos e objetos. O EE consome as seguintes interfaces, que são implementadas pelo DE:

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  O EE executa [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md). `IDebugProperty2` fornece o mecanismo para descrever o resultado de uma avaliação de expressão, como uma variável local, um primitivo ou um objeto para o Visual Studio, que exibe as informações apropriadas na janela **locais**, **inspecionar** ou **imediato** .

  O SP é fornecido ao EE pelo DE quando ele solicita informações. O SP executa interfaces que descrevem endereços e campos, como as seguintes interfaces e seus derivados:

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  O EE consome todas essas interfaces.

## <a name="in-this-section"></a>Nesta seção
 [Estratégia de implementação do avaliador de expressão](../../extensibility/debugger/expression-evaluator-implementation-strategy.md) Define um processo de três etapas para a estratégia de implementação do avaliador de expressão (EE).

## <a name="see-also"></a>Confira também
- [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
