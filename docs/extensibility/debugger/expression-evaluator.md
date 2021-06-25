---
title: Avaliador de expressão | Microsoft Docs
description: Saiba mais sobre os avaliadores de expressão, que examinam a sintaxe de uma linguagem para analisar e avaliar variáveis e expressões em runtime no modo de quebra.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 998f361d8008257cb8f4a888b4d4fbb985c9c977
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900974"
---
# <a name="expression-evaluator"></a>Avaliador de expressão
Os avaliadores de expressão (EE) examinam a sintaxe de uma linguagem para analisar e avaliar variáveis e expressões em tempo de executar, permitindo que eles sejam exibidos pelo usuário quando o IDE estiver no modo de quebra.

## <a name="use-expression-evaluators"></a>Usar avaliadores de expressão
 As expressões são criadas usando [o método ParseText,](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) da seguinte forma:

1. O DE (mecanismo de depuração) implementa a interface [IDebugExpressionContext2.](../../extensibility/debugger/reference/idebugexpressioncontext2.md)

2. O pacote de depuração obtém um objeto de uma `IDebugExpressionContext2` interface [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) e, em seguida, chama o método nele para obter `IDebugStackFrame2::ParseText` um objeto [IDebugExpression2.](../../extensibility/debugger/reference/idebugexpression2.md)

3. O pacote de depuração chama [o método EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) ou [o método EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) para obter o valor da expressão. `IDebugExpression2::EvaluateAsync` é chamado na janela Comando/Imediato. Todos os outros componentes da interface do usuário chamam `IDebugExpression2::EvaluateSync` .

4. O resultado da avaliação de expressão é um objeto [IDebugProperty2,](../../extensibility/debugger/reference/idebugproperty2.md) que contém o nome, o tipo e o valor do resultado da avaliação da expressão.

   Durante a avaliação da expressão, o EE requer informações do componente do provedor de símbolos. O provedor de símbolos fornece as informações simbólicas usadas para identificar e entender a expressão analisado.

   Quando a avaliação de expressão assíncrona é concluída, um evento assíncrono é enviado pelo DE por meio do SDM (gerenciador de depuração de sessão) para notificar o IDE de que a avaliação de expressão foi concluída. E, o resultado da avaliação é retornado da chamada para o `IDebugExpression2::EvaluateSync` método .

## <a name="implementation-notes"></a>Notas de implementação
 Os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] mecanismos de depuração esperam conversar com o avaliador de expressão usando interfaces CLR (Common Language Runtime). Como resultado, um avaliador de expressão que funciona com os mecanismos de depuração deve dar suporte ao CLR (uma lista completa de todas as interfaces de depuração CLR pode ser encontrada no debugref.doc, que faz parte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] do [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] ).

## <a name="see-also"></a>Confira também
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
