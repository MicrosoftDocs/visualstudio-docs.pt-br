---
title: Escrevendo um avaliador de expressão Common Language Runtime | Microsoft Docs
description: Saiba mais sobre como escrever um avaliador de expressão para o Common Language Runtime, que avalia as expressões na linguagem de código que está sendo depurada.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 658158785d8f8a9376f5357ae2b869f6ad2e2271
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091390"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>Escrevendo um avaliador de expressão de Common Language Runtime
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 O avaliador de expressão (EE) é a parte de um mecanismo de depuração (DE) que manipula a sintaxe e a semântica da linguagem de programação que produziu o código que está sendo depurado. As expressões devem ser avaliadas no contexto de uma linguagem de programação. Por exemplo, em alguns idiomas, a expressão "a + B" significa "a soma de A e B". Em outros idiomas, a mesma expressão pode significar "A ou B". Portanto, um EE separado deve ser escrito para cada linguagem de programação que gera código de objeto a ser depurado no IDE do Visual Studio.

 Alguns aspectos do pacote de depuração do Visual Studio devem interpretar o código no contexto da linguagem de programação. Por exemplo, quando a execução é interrompida em um ponto de interrupção, todas as expressões que o usuário tiver digitado em uma janela de **inspeção** devem ser avaliadas e exibidas. O usuário pode alterar o valor de uma variável local digitando uma expressão em uma janela de **inspeção** ou na janela **imediata** .

## <a name="in-this-section"></a>Nesta seção
 [Tempo de execução de linguagem comum e avaliação de expressão](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md) Explica que quando você está integrando a linguagem de programação proprietária no IDE do Visual Studio, escrever um EE capaz de avaliar expressões dentro do contexto da linguagem proprietária permite que você compile para uma MSIL (Microsoft Intermediate Language) sem escrever um mecanismo de depuração.

 [Arquitetura do avaliador de expressão](../../extensibility/debugger/expression-evaluator-architecture.md) Discute como implementar as interfaces de EE necessárias e chamar o provedor de símbolo de Common Language Runtime (SP) e as interfaces de fichário.

 [Registrar um avaliador de expressão](../../extensibility/debugger/registering-an-expression-evaluator.md) Observa que o EE deve se registrar como uma fábrica de classes com os ambientes de tempo de execução do Common Language Runtime e do Visual Studio.

 [Implementar um avaliador de expressão](../../extensibility/debugger/implementing-an-expression-evaluator.md) Descreve como o processo de avaliação de uma expressão inclui o mecanismo de depuração (DE), o provedor de símbolos (SP), o objeto de fichário e o avaliador de expressão (EE).

 [Exibir locais](../../extensibility/debugger/displaying-locals.md) Descreve como, quando a execução pausa, o pacote de depuração chama o DE para obter uma lista de variáveis e argumentos locais.

 [Avaliar uma expressão de janela de inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md) Documenta como o pacote de depuração do Visual Studio chama de DE para determinar o valor atual de cada expressão em sua lista de observação.

 [Alterar o valor de um local](../../extensibility/debugger/changing-the-value-of-a-local.md) Explica que, ao alterar o valor de um local, cada linha da janela locais tem um objeto associado que fornece o nome, o tipo e o valor atual de um local.

 [Implementar visualizadores de tipo e visualizadores personalizados](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md) Explica qual interface precisa ser implementada por qual componente para dar suporte a visualizadores de tipo e espectadores personalizados.

## <a name="see-also"></a>Confira também
 [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
