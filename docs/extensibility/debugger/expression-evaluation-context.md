---
title: Contexto de avaliação de expressão | Microsoft Docs
description: Saiba mais sobre o contexto de avaliação de expressão, que representa um contexto para avaliação de expressão e existe quando um programa é interrompido em um ponto de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73eeafb95c7e4d52f69109c5eb7c06eb48bd8d88
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901208"
---
# <a name="expression-evaluation-context"></a>Contexto de avaliação de expressão
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, um contexto **de avaliação de expressão**:

- Representa um contexto para avaliação de expressão. Em geral, um contexto de avaliação corresponde ao escopo léxico no qual avaliar variáveis, parâmetros, funções e métodos. Por exemplo, um contexto de avaliação de expressão associado a um quadro de pilha fornecerá o contexto para avaliar variáveis locais, parâmetros de método e membros de classe (se aplicável).

- Existe quando um programa é interrompido em um ponto de interrupção. A expressão em si é uma estrutura de dados que representa uma expressão analisado que está pronta para associação e avaliação dentro do contexto determinado.

     Mais detalhadamente, as expressões são criadas usando o [método ParseText.](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) Quando uma expressão é avaliada, ela gera uma cadeia de caracteres imprimível que contém o nome e o tipo de variável ou argumento e seu valor. Essa cadeia de caracteres é exibida no janela Inspeção ou na janela Locais do IDE.

     Dado um e uma `BSTR` interface [IDebugExpressionContext2,](../../extensibility/debugger/reference/idebugexpressioncontext2.md) um DE (mecanismo de depuração) pode criar uma interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) ao analisar uma expressão. Dada uma interface, a DE pode obter um valor por meio da avaliação de expressão `IDebugExpression2` síncrona ou assíncrona. Esse valor, juntamente com o nome e o tipo da variável ou argumento, é enviado para o IDE para exibição.

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
