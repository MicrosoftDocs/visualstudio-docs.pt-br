---
title: Contexto de avaliação da expressão | Microsoft Docs
description: Saiba mais sobre o contexto de avaliação de expressão, que representa um contexto para avaliação de expressão e existe quando um programa foi interrompido em um ponto de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 249510349d831f4f00578e36200f0d236d83ef59
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096831"
---
# <a name="expression-evaluation-context"></a>Contexto de avaliação da expressão
Em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, um **contexto de avaliação de expressão**:

- Representa um contexto para avaliação de expressão. Em geral, um contexto de avaliação corresponde ao escopo léxico no qual avaliar variáveis, parâmetros, funções e métodos. Por exemplo, um contexto de avaliação de expressão associado a um quadro de pilha fornecerá o contexto para avaliar variáveis locais, parâmetros de método e membros de classe (se aplicável).

- Existe quando um programa é interrompido em um ponto de interrupção. A própria expressão é uma estrutura de dados que representa uma expressão analisada que está pronta para associação e avaliação dentro do contexto especificado.

     Mais detalhadamente, as expressões são criadas usando o método [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) . Quando uma expressão é avaliada, ela gera uma cadeia de caracteres imprimível que contém o nome e o tipo de variável ou argumento e seu valor. Essa cadeia de caracteres é exibida no janela Inspeção ou na janela locais do IDE.

     Dado um `BSTR` e uma interface [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) , um mecanismo DE depuração (de) pode criar uma interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) analisando uma expressão. Dada uma `IDebugExpression2` interface, o de pode obter um valor por meio de avaliação de expressão assíncrona ou síncrono. Esse valor, junto com o nome e o tipo da variável ou argumento, é enviado para o IDE para exibição.

## <a name="see-also"></a>Confira também
- [Interfaces de avaliação de expressão](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
