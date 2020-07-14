---
title: Alterando o valor de um local | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 565ae9f27b9f5a113e51520724f525599ad5eda7
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904270"
---
# <a name="change-the-value-of-a-local"></a>Alterar o valor de um local
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Quando um novo valor é digitado no campo valor da janela **locais** , o pacote de depuração passa a cadeia de caracteres, conforme digitado, para o avaliador de expressão (EE). O EE avalia essa cadeia de caracteres, que pode conter um valor simples ou uma expressão, e armazena o valor resultante no local associado.

 Esta é uma visão geral do processo de alteração do valor de um local:

1. Depois que o usuário insere o novo valor, o Visual Studio chama [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) no objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) associado ao local.

2. `IDebugProperty2::SetValueAsString` realiza as seguintes tarefas:

   1. Avalia a cadeia de caracteres para produzir um valor.

   2. Associa o objeto [IDebugField](../../extensibility/debugger/reference/idebugfield.md) associado para obter um objeto [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) .

   3. Converte o valor em uma série de bytes.

   4. Chama [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md) para colocar os bytes do valor na memória para que o programa que está sendo depurado possa acessá-los.

3. O Visual Studio atualiza a exibição de **locais** (consulte [exibindo locais](../../extensibility/debugger/displaying-locals.md) para obter detalhes).

   Esse procedimento também é usado para alterar o valor de uma variável na janela **Watch** , exceto que é o `IDebugProperty2` objeto associado ao valor do local que é usado em vez do `IDebugProperty2` objeto associado ao próprio local.

## <a name="in-this-section"></a>Nesta seção
 [Exemplo de implementação de valores de alteração](../../extensibility/debugger/sample-implementation-of-changing-values.md) Usa o exemplo MyCEE para percorrer o processo de alteração de valores.

## <a name="see-also"></a>Confira também
- [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)
