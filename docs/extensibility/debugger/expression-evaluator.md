---
title: Avaliador de expressão | Microsoft Docs
description: Saiba mais sobre avaliadores de expressão, que examinam a sintaxe de um idioma para analisar e avaliar variáveis e expressões em tempo de execução no modo de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6876bea4174df7f5ac293ea0d470f5922d7492d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055018"
---
# <a name="expression-evaluator"></a>Avaliador de expressão
Os avaliadores de expressão (EE) examinam a sintaxe de um idioma para analisar e avaliar variáveis e expressões em tempo de execução, permitindo que eles sejam exibidos pelo usuário quando o IDE estiver no modo de interrupção.

## <a name="use-expression-evaluators"></a>Usar avaliadores de expressão
 As expressões são criadas usando o método [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) , da seguinte maneira:

1. O mecanismo de depuração (DE) implementa a interface [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) .

2. O pacote de depuração Obtém um `IDebugExpressionContext2` objeto de uma interface [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) e, em seguida, chama o `IDebugStackFrame2::ParseText` método nele para obter um objeto [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) .

3. O pacote de depuração chama o método [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou o método [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter o valor da expressão. `IDebugExpression2::EvaluateAsync` é chamado na janela comando/imediato. Todos os outros componentes da interface do usuário chamam `IDebugExpression2::EvaluateSync` .

4. O resultado da avaliação de expressão é um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) , que contém o nome, o tipo e o valor do resultado da avaliação da expressão.

   Durante a avaliação da expressão, o EE requer informações do componente de provedor de símbolo. O provedor de símbolos fornece as informações simbólicas usadas para identificar e compreender a expressão analisada.

   Quando a avaliação de expressão assíncrona é concluída, um evento assíncrono é enviado pelo por meio do SDM (Gerenciador de depuração de sessão) para notificar o IDE de que a avaliação da expressão foi concluída. E, em seguida, o resultado da avaliação é retornado da chamada para o `IDebugExpression2::EvaluateSync` método.

## <a name="implementation-notes"></a>Notas de implementação
 Os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] mecanismos de depuração esperam conversar com o avaliador de expressão usando interfaces CLR (Common Language Runtime). Como resultado, um avaliador de expressão que funciona com os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] mecanismos de depuração deve dar suporte ao CLR (uma lista completa de todas as interfaces de depuração de CLR pode ser encontrada em debugref.doc, que faz parte do [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] ).

## <a name="see-also"></a>Confira também
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
